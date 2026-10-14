# SEAS 8525 Code & Logic

38 worked NumPy examples. Each snippet was run, and its real output is shown below the code.

## Class 1 · Introduction to Generative AI

### Maximum likelihood for the uniform-box model

1. A box θ = (x1, y1, x2, y2) defines a uniform density: 1/area inside the box, 0 outside.
2. For independent points, log L(θ) = Σ log p_θ(x_i) = n · log(1/area) if every point is inside, and −∞ otherwise.
3. So a box that misses even one point is impossible (likelihood 0). Among boxes that cover everything, the smaller the area, the higher the likelihood.
4. So the MLE is the tightest bounding box of the data. Bigger boxes are valid but less likely, and a box missing any point is ruled out.

```python
import numpy as np
rng = np.random.default_rng(0)
X = rng.uniform([-3, 1], [4, 5], size=(200, 2))        # data from an unknown box

def log_lik(box, X):
    x1, y1, x2, y2 = box
    inside = (X[:, 0] >= x1) & (X[:, 0] <= x2) & (X[:, 1] >= y1) & (X[:, 1] <= y2)
    if not inside.all():
        return -np.inf                                   # one zero factor kills the product
    area = (x2 - x1) * (y2 - y1)
    return len(X) * np.log(1 / area)

tight = (*X.min(0), *X.max(0))
for name, box in [("left half only", (-3, 1, 0.5, 5)),
                  ("huge box", (-10, -10, 10, 10)),
                  ("tight box (MLE)", tight)]:
    print(f"{name:16s} log L = {log_lik(box, X):10.2f}")
```

Output:

```
left half only   log L =       -inf
huge box         log L =   -1198.29
tight box (MLE)  log L =    -663.55
```

### Why we maximize the log-likelihood

1. Multiplying many probabilities below 1 shrinks the result toward 0 exponentially fast.
2. 64-bit floats cannot represent anything below about 1e-308, so the product underflows to exactly 0 and the gradient disappears.
3. log is strictly increasing, so argmax of Σ log p equals argmax of ∏ p, and the sum stays in a normal numeric range.

```python
import numpy as np
rng = np.random.default_rng(1)
p = rng.uniform(0.01, 0.5, size=1000)   # per-point densities of 1,000 observations
print("product of probabilities :", np.prod(p))
print("sum of log-probabilities :", np.sum(np.log(p)).round(2))
```

Output:

```
product of probabilities : 0.0
sum of log-probabilities : -1599.99
```

### Generative vs discriminative: who can sample?

1. A generative model fits p(x | y) and p(y). By Bayes’ rule it can also give p(y | x), and it can sample new x.
2. A discriminative model fits only p(y | x). It has no distribution over x, so there is nothing to sample new data from.
3. Below, two 1-D classes are modeled with Gaussians (generative). We classify with Bayes’ rule and then draw new class-1 samples.

```python
import numpy as np
rng = np.random.default_rng(2)
x0 = rng.normal(-2, 1.0, 300); x1 = rng.normal(3, 0.7, 300)

# generative fit: p(x|y) Gaussian per class, p(y) from counts
mu = [x0.mean(), x1.mean()]; sd = [x0.std(), x1.std()]; prior = [0.5, 0.5]
pdf = lambda x, m, s: np.exp(-(x - m)**2 / (2 * s * s)) / (s * np.sqrt(2 * np.pi))

x = 0.8
joint = [pdf(x, mu[k], sd[k]) * prior[k] for k in (0, 1)]
print("p(y=1 | x=0.8) via Bayes:", round(joint[1] / sum(joint), 4))
print("new samples from p(x | y=1):", rng.normal(mu[1], sd[1], 5).round(2))
# a logistic regression would give only the first number, never the second
```

Output:

```
p(y=1 | x=0.8) via Bayes: 0.3478
new samples from p(x | y=1): [3.4  3.29 2.81 3.08 4.75]
```

## Class 2 · Deep Learning (Vision ↔ NLP)

### Counting parameters and output shapes

1. Each conv filter spans the whole input depth: k_h·k_w·C_in weights plus 1 bias. The layer has one filter per output channel.
2. Dense layers have in·out weights plus out biases. Flatten and pooling only rearrange or select values, so they have 0 parameters.
3. Output size: ‘valid’ gives ⌊(H−k)/s⌋+1. ‘same’ gives ⌈H/s⌉, so stride 2 halves the size each time.

```python
import math
conv  = lambda k, cin, f, bias=True: (k * k * cin + bias) * f
dense = lambda i, o: i * o + o

print("5 filters 4x4 on 3 ch (no bias):", conv(4, 3, 5, bias=False))
layers = [conv(4, 3, 10), conv(3, 10, 20), 0, dense(1280, 10)]
print("example CNN per layer:", layers, "total:", sum(layers))
print("3x3, 64 -> 128 with bias:", conv(3, 64, 128))

# autoencoder encoder: 32x32x1 -> three stride-2 'same' convs
h = 32
for f in (32, 64, 128):
    h = math.ceil(h / 2); print(f"after conv({f}) -> {h}x{h}x{f}")
print("flatten:", h * h * 128, "| Dense(2) params:", dense(h * h * 128, 2))
```

Output:

```
5 filters 4x4 on 3 ch (no bias): 240
example CNN per layer: [490, 1820, 0, 12810] total: 15120
3x3, 64 -> 128 with bias: 73856
after conv(32) -> 16x16x32
after conv(64) -> 8x8x64
after conv(128) -> 4x4x128
flatten: 2048 | Dense(2) params: 4098
```

### Convolution and max pooling from scratch

1. A convolution slides one small weight matrix over the image and takes a dot product at each position.
2. The same weights are reused everywhere (weight sharing). That is why a CNN needs few parameters and detects a pattern wherever it appears.
3. A vertical-edge kernel responds only where intensity changes left to right. Max pooling then keeps the strongest response in each 2×2 block.

```python
import numpy as np
img = np.zeros((6, 6)); img[:, 3:] = 1.0          # dark left half, bright right half
k = np.array([[-1, 0, 1]] * 3, dtype=float)       # vertical edge detector

def conv2d(x, k):                                  # 'valid', stride 1
    H, W = x.shape[0] - k.shape[0] + 1, x.shape[1] - k.shape[1] + 1
    return np.array([[np.sum(x[i:i+3, j:j+3] * k) for j in range(W)] for i in range(H)])

fmap = conv2d(img, k)
print("feature map:\n", fmap)
pooled = fmap.reshape(2, 2, 2, 2).max(axis=(1, 3))  # 2x2 max pooling
print("after 2x2 max pool:\n", pooled)
```

Output:

```
feature map:
 [[0. 3. 3. 0.]
 [0. 3. 3. 0.]
 [0. 3. 3. 0.]
 [0. 3. 3. 0.]]
after 2x2 max pool:
 [[3. 3.]
 [3. 3.]]
```

### Why skip connections keep gradients alive

1. Backprop through L layers multiplies L Jacobians. If each one shrinks a vector by a factor below 1, the gradient decays geometrically.
2. With a skip, each block is x + F(x), so its Jacobian is I + J_F. The identity term passes the gradient through even when J_F is small.
3. Below: 50 random layers with small weights. The plain chain’s gradient norm collapses toward 0, while the residual chain’s stays of order 1.

```python
import numpy as np
rng = np.random.default_rng(3)
d, L = 64, 50
g_plain = g_res = np.ones(d) / np.sqrt(d)            # gradient arriving at the top
for _ in range(L):
    J = rng.normal(0, 0.2 / np.sqrt(d), (d, d))      # small layer Jacobian
    g_plain = J.T @ g_plain                           # plain: f(x) = C(x)
    g_res = (np.eye(d) + J).T @ g_res                 # residual: f(x) = C(x) + x
print(f"plain    |grad| after {L} layers: {np.linalg.norm(g_plain):.2e}")
print(f"residual |grad| after {L} layers: {np.linalg.norm(g_res):.2e}")
```

Output:

```
plain    |grad| after 50 layers: 5.94e-36
residual |grad| after 50 layers: 2.47e+00
```

### Precision, recall and F1 from a confusion count

1. Precision = TP/(TP+FP), recall = TP/(TP+FN).
2. F1 is the harmonic mean, 2PR/(P+R). It is pulled toward the smaller of the two, so a classifier cannot hide poor recall behind high precision.

```python
TP, FP, FN = 40, 5, 35
P, R = TP / (TP + FP), TP / (TP + FN)
print(f"precision={P:.3f} recall={R:.3f}")
print(f"arithmetic mean={(P + R) / 2:.3f}  F1 (harmonic)={2 * P * R / (P + R):.3f}")
```

Output:

```
precision=0.889 recall=0.533
arithmetic mean=0.711  F1 (harmonic)=0.667
```

### Transfer learning vs fine-tuning in Keras

1. Transfer learning: keep the pretrained feature extractor frozen and train only a new head, so few parameters are learned from little data.
2. Fine-tuning: then unfreeze some or all layers and continue training with a much smaller learning rate, so the pretrained features shift gently instead of being overwritten (catastrophic forgetting).
3. This snippet is for reading only; it needs TensorFlow, so it was not executed here.

```python
# (not executed here: requires TensorFlow)
import tensorflow as tf
base = tf.keras.applications.ResNet50(include_top=False, weights="imagenet", pooling="avg")
base.trainable = False                                  # 1) freeze feature extractor
model = tf.keras.Sequential([base, tf.keras.layers.Dense(5, activation="softmax")])  # 2) new head
model.compile(tf.keras.optimizers.Adam(1e-3), "sparse_categorical_crossentropy")
# model.fit(train_ds, epochs=5)                         # trains only the head

base.trainable = True                                   # 3) fine-tune
for layer in base.layers[:-30]:
    layer.trainable = False                             # keep early, generic layers frozen
model.compile(tf.keras.optimizers.Adam(1e-5), "sparse_categorical_crossentropy")  # 100x smaller LR
# model.fit(train_ds, epochs=5)
```

## SimCLR paper (Chen et al., 2020)

### NT-Xent loss in NumPy

1. Embed 2N views (two per image), ℓ2-normalize them, and compute all pairwise cosine similarities divided by τ.
2. For row i, the positive is its partner view. The other 2N−2 views are negatives; the self-similarity is masked out.
3. The loss is cross-entropy where the ‘correct class’ is the partner. Aligned pairs give a loss near 0. Random embeddings give a high loss: uniform guessing would be log(2N−1), and with τ = 0.1 random similarities are amplified, so it is even worse.

```python
import numpy as np
def nt_xent(z, tau=0.1):
    z = z / np.linalg.norm(z, axis=1, keepdims=True)    # l2-normalize -> cosine sim
    n2 = len(z); N = n2 // 2
    sim = z @ z.T / tau
    np.fill_diagonal(sim, -np.inf)                      # exclude k == i
    pos = np.r_[np.arange(N, n2), np.arange(N)]         # partner of i is i +/- N
    logprob = sim[np.arange(n2), pos] - np.log(np.exp(sim).sum(1))
    return -logprob.mean()

rng = np.random.default_rng(4); N, d = 8, 32
base = rng.normal(size=(N, d))
aligned = np.r_[base, base + 0.05 * rng.normal(size=(N, d))]   # views agree
random_ = rng.normal(size=(2 * N, d))                           # views unrelated
print("negatives per positive pair: 2(N-1) =", 2 * (N - 1))
print("loss, aligned views:", nt_xent(aligned).round(3))
print("loss, random views :", nt_xent(random_).round(3), "| log(2N-1) =", np.log(2 * N - 1).round(3))
```

Output:

```
negatives per positive pair: 2(N-1) = 14
loss, aligned views: 0.003
loss, random views : 3.716 | log(2N-1) = 2.708
```

### What the temperature τ does

1. Softmax over similarity/τ. A small τ sharpens the distribution, so the hardest negatives (highest similarity) dominate the gradient.
2. A large τ flattens it, so all negatives get similar weight and easy negatives waste signal.
3. This is why NT-Xent needs no explicit hard-negative mining: τ does the weighting.

```python
import numpy as np
sims = np.array([0.9, 0.6, 0.3, 0.0, -0.3])   # cosine sims of 5 negatives to an anchor
for tau in (1.0, 0.5, 0.1):
    w = np.exp(sims / tau); w /= w.sum()
    print(f"tau={tau:<4} weights={w.round(3)}")
```

Output:

```
tau=1.0  weights=[0.334 0.247 0.183 0.136 0.1  ]
tau=0.5  weights=[0.475 0.261 0.143 0.078 0.043]
tau=0.1  weights=[0.95  0.047 0.002 0.    0.   ]
```

## Class 3 · Autoencoders & VAEs

### Mixture of Gaussians: ancestral sampling and marginal density

1. Sample in factorization order: first the discrete latent z ~ Categorical(λ), then x ~ N(μ_z, σ_z²).
2. The marginal is Pr(x) = Σ_n λ_n N(x; μ_n, σ_n²), a weighted sum of bumps that can have several peaks.
3. A histogram of the ancestral samples matches this marginal density.

```python
import numpy as np
rng = np.random.default_rng(5)
lam, mu, sd = np.array([0.7, 0.2, 0.1]), np.array([-2., 1., 4.]), np.array([0.6, 0.4, 0.8])

z = rng.choice(3, size=100_000, p=lam)          # 1) z ~ Pr(z)
x = rng.normal(mu[z], sd[z])                    # 2) x ~ Pr(x | z)

def marginal(t):                                # Pr(x) = sum_n lam_n N(x; mu_n, sd_n)
    return np.sum(lam * np.exp(-(t - mu)**2 / (2 * sd**2)) / (sd * np.sqrt(2 * np.pi)))

for t in (-2, 1, 4):
    emp = np.mean(np.abs(x - t) < 0.05) / 0.1   # histogram density near t
    print(f"x={t:+d}: formula {marginal(t):.3f}  vs samples {emp:.3f}")
```

Output:

```
x=-2: formula 0.465  vs samples 0.469
x=+1: formula 0.200  vs samples 0.200
x=+4: formula 0.050  vs samples 0.047
```

### Closed-form KL vs a Monte Carlo check

1. For q = N(μ, σ²) and p = N(0, 1): KL(q‖p) = ½(μ² + σ² − log σ² − 1) per dimension.
2. With log_var = log σ², this is −½(1 + log_var − μ² − e^{log_var}), the formula used in Keras VAE code.
3. We check it by averaging log q(z) − log p(z) over samples from q. Note it is 0 only at μ = 0, σ = 1.

```python
import numpy as np
rng = np.random.default_rng(6)
def kl_closed(mu, log_var):
    return -0.5 * np.sum(1 + log_var - mu**2 - np.exp(log_var))

def kl_mc(mu, log_var, n=400_000):
    s = np.exp(0.5 * log_var); z = mu + s * rng.standard_normal(n)
    log_q = -0.5 * ((z - mu) / s)**2 - np.log(s) - 0.5 * np.log(2 * np.pi)
    log_p = -0.5 * z**2 - 0.5 * np.log(2 * np.pi)
    return np.mean(log_q - log_p)

for mu, lv in [(0.0, 0.0), (1.5, 0.0), (0.0, np.log(0.2)), (-1.0, np.log(3.0))]:
    print(f"mu={mu:+.1f} var={np.exp(lv):.1f}  closed={kl_closed(mu, lv):.4f}  MC={kl_mc(mu, lv):.4f}")
```

Output:

```
mu=+0.0 var=1.0  closed=-0.0000  MC=0.0000
mu=+1.5 var=1.0  closed=1.1250  MC=1.1256
mu=+0.0 var=0.2  closed=0.4047  MC=0.4033
mu=-1.0 var=3.0  closed=0.9507  MC=0.9512
```

### Reparameterization: gradients through sampling

1. We want ∂/∂μ E_{z~N(μ,σ²)}[f(z)]. Sampling z directly is not differentiable in μ.
2. Write z = μ + σ·ε with ε ~ N(0,1). Then ∂f(z)/∂μ = f′(z)·1, which we can average over ε.
3. For f(z) = z², the true gradient is 2μ. The reparameterized estimate matches it. σ = exp(0.5·log_var) is always positive, which is why the encoder outputs log_var.

```python
import numpy as np
rng = np.random.default_rng(7)
mu, log_var = 1.3, np.log(0.5)
sigma = np.exp(0.5 * log_var)                 # always > 0, whatever log_var is
eps = rng.standard_normal(200_000)
z = mu + sigma * eps                          # z is now a differentiable function of mu
grad_est = np.mean(2 * z * 1.0)               # df/dz * dz/dmu, with f(z) = z^2
print("reparam estimate d/dmu E[z^2]:", grad_est.round(4), "| exact 2*mu:", 2 * mu)
```

Output:

```
reparam estimate d/dmu E[z^2]: 2.6013 | exact 2*mu: 2.6
```

### The ELBO is tight only when q is the true posterior

1. Model: z ~ N(0, 1), x | z ~ N(z, s²). Then log p(x) is known exactly: x ~ N(0, 1 + s²).
2. ELBO(q) = E_q[log p(x|z)] − KL(q‖p(z)) = log p(x) − KL(q‖p(z|x)), so it is always ≤ log p(x).
3. Set q to the exact posterior and the gap is 0. Any other q (wrong mean or variance) gives a strictly lower bound.

```python
import numpy as np
s2, x = 0.5, 1.2
log_px = -0.5 * np.log(2 * np.pi * (1 + s2)) - x**2 / (2 * (1 + s2))

def elbo(m, v):                               # q(z) = N(m, v); expectations in closed form
    exp_loglik = -0.5 * np.log(2 * np.pi * s2) - ((x - m)**2 + v) / (2 * s2)
    kl = 0.5 * (m**2 + v - np.log(v) - 1)
    return exp_loglik - kl

post_m, post_v = x / (1 + s2), s2 / (1 + s2)  # exact Gaussian posterior
print(f"log p(x)               = {log_px:.4f}")
print(f"ELBO, q = posterior    = {elbo(post_m, post_v):.4f}")
print(f"ELBO, q = prior N(0,1) = {elbo(0.0, 1.0):.4f}")
print(f"ELBO, q = N(1.5, 0.1)  = {elbo(1.5, 0.1):.4f}")
```

Output:

```
log p(x)               = -1.6017
ELBO, q = posterior    = -1.6017
ELBO, q = prior N(0,1) = -3.0124
ELBO, q = N(1.5, 0.1)  = -2.5887
```

### Why a VAE latent space has no gaps

1. A plain AE maps each input to one point. Nothing in the loss cares about the space between points, so the decoder is untrained there.
2. A VAE encodes each input as N(μ, σ²) and decodes a sample from it, so the decoder must handle a whole neighborhood. The KL term pulls every region toward N(0, I).
3. Measure: what fraction of random prior samples land near some training code? The VAE regions cover the prior; the AE points leave most of it empty.

```python
import numpy as np
rng = np.random.default_rng(8)
n = 300
ae_codes = rng.normal([3, 6], [2.5, 1.5], (n, 2))           # uneven, off-center points (no KL)
vae_mu = rng.normal(0, 0.8, (n, 2)); vae_sd = 0.6           # centered, each with a fuzzy region

probe = rng.standard_normal((2000, 2))                      # where we sample at generation time
def covered(centers, radius):
    d = np.linalg.norm(probe[:, None] - centers[None], axis=2).min(1)
    return np.mean(d < radius)
print("prior samples near an AE code   :", covered(ae_codes, 0.3))
print("prior samples inside a VAE region:", covered(vae_mu, 2 * vae_sd))
```

Output:

```
prior samples near an AE code   : 0.0045
prior samples inside a VAE region: 0.9945
```

## Class 4 · Transformers

### Scaled dot-product attention with a causal mask

1. Project the inputs: Q = XW_Q, K = XW_K, V = XW_V. Only these W matrices are learned.
2. Scores S = QKᵀ/√d_k form an n×n matrix. A causal mask sets S[i, j] = −∞ for j > i.
3. Row-wise softmax turns scores into weights (non-negative, summing to 1, with zeros above the diagonal). The output Z = weights·V.

```python
import numpy as np
rng = np.random.default_rng(9)
n, d_model, d_k = 5, 16, 8
X = rng.normal(size=(n, d_model))
Wq, Wk, Wv = (rng.normal(size=(d_model, d_k)) / np.sqrt(d_model) for _ in range(3))
Q, K, V = X @ Wq, X @ Wk, X @ Wv

S = Q @ K.T / np.sqrt(d_k)                         # (n, n) score matrix
S[np.triu_indices(n, k=1)] = -np.inf               # causal mask: no peeking ahead
W = np.exp(S - S.max(1, keepdims=True)); W /= W.sum(1, keepdims=True)
Z = W @ V
np.set_printoptions(precision=2, suppress=True)
print("attention weights (row i = query i):\n", W)
print("row sums:", W.sum(1), "| output shape:", Z.shape)
```

Output:

```
attention weights (row i = query i):
 [[1.   0.   0.   0.   0.  ]
 [0.62 0.38 0.   0.   0.  ]
 [0.35 0.23 0.42 0.   0.  ]
 [0.11 0.11 0.53 0.24 0.  ]
 [0.   0.04 0.13 0.75 0.08]]
row sums: [1. 1. 1. 1. 1.] | output shape: (5, 8)
```

### Why divide by √d_k

1. If q and k have independent unit-variance entries, q·k is a sum of d_k terms, so its variance is d_k.
2. Large logits saturate the softmax into a near one-hot output, where gradients are almost 0.
3. Dividing by √d_k brings the variance back to about 1 and keeps the softmax in its sensitive range.

```python
import numpy as np
rng = np.random.default_rng(10)
for d_k in (4, 64, 512):
    q, k = rng.standard_normal((2, 10_000, d_k))
    dots = np.sum(q * k, axis=1)
    row = dots[:16]                                  # 16 keys competing for one query
    sm = lambda s: np.exp(s - s.max()) / np.exp(s - s.max()).sum()
    print(f"d_k={d_k:3d} var(q.k)={dots.var():7.1f}  max softmax weight: raw={sm(row).max():.2f}"
          f"  scaled={sm(row / np.sqrt(d_k)).max():.2f}")
```

Output:

```
d_k=  4 var(q.k)=    4.1  max softmax weight: raw=0.34  scaled=0.19
d_k= 64 var(q.k)=   63.7  max softmax weight: raw=0.93  scaled=0.19
d_k=512 var(q.k)=  521.8  max softmax weight: raw=1.00  scaled=0.29
```

### Sinusoidal positional encoding: relative position is a linear map

1. PE(pos, 2i) = sin(pos·ω_i) and PE(pos, 2i+1) = cos(pos·ω_i), with ω_i = 1/10000^{2i/d}.
2. Each (sin, cos) pair is a point on a circle. Shifting the position by k rotates it by angle k·ω_i.
3. So PE(pos + k) = R_k · PE(pos) with a block-diagonal rotation matrix R_k that does not depend on pos. Attention can therefore learn relative offsets with a linear map.

```python
import numpy as np
def pe(pos, d=16):
    i = np.arange(d // 2); w = 1 / 10000 ** (2 * i / d)
    out = np.empty(d); out[0::2] = np.sin(pos * w); out[1::2] = np.cos(pos * w)
    return out

def R(k, d=16):                                  # rotation by k*w_i in each (sin, cos) pair
    i = np.arange(d // 2); w = 1 / 10000 ** (2 * i / d); M = np.zeros((d, d))
    for j, a in enumerate(k * w):
        M[2*j:2*j+2, 2*j:2*j+2] = [[np.cos(a), np.sin(a)], [-np.sin(a), np.cos(a)]]
    return M

k = 7
for pos in (0, 3, 40):
    err = np.abs(R(k) @ pe(pos) - pe(pos + k)).max()
    print(f"pos={pos:2d}: max |R_k PE(pos) - PE(pos+k)| = {err:.1e}")
```

Output:

```
pos= 0: max |R_k PE(pos) - PE(pos+k)| = 0.0e+00
pos= 3: max |R_k PE(pos) - PE(pos+k)| = 2.2e-16
pos=40: max |R_k PE(pos) - PE(pos+k)| = 3.3e-16
```

### Multi-head attention shapes and parameter count

1. Split d_model into h heads of size d_model/h. Each head runs attention in its own subspace.
2. Concatenate the h outputs back to d_model and mix them with W_O.
3. Parameters: W_Q, W_K, W_V and W_O are each d_model×d_model, so 4·d² weights. That is the same total regardless of h.

```python
import numpy as np
rng = np.random.default_rng(11)
n, d, h = 6, 768, 12
dh = d // h
X = rng.normal(size=(n, d))
Wq, Wk, Wv, Wo = (rng.normal(size=(d, d)) / np.sqrt(d) for _ in range(4))

def split(M): return M.reshape(n, h, dh).transpose(1, 0, 2)       # (h, n, dh)
Q, K, V = split(X @ Wq), split(X @ Wk), split(X @ Wv)
S = Q @ K.transpose(0, 2, 1) / np.sqrt(dh)
A = np.exp(S - S.max(-1, keepdims=True)); A /= A.sum(-1, keepdims=True)
heads = A @ V                                                   # (h, n, dh)
out = heads.transpose(1, 0, 2).reshape(n, d) @ Wo
print("head dim:", dh, "| per-head output:", heads.shape, "| final:", out.shape)
print("attention weights (no biases): 4*d^2 =", 4 * d * d)
```

Output:

```
head dim: 64 | per-head output: (12, 6, 64) | final: (6, 768)
attention weights (no biases): 4*d^2 = 2359296
```

### Layer norm vs batch norm: which axis?

1. Batch norm averages each feature across the batch, so a sample’s output depends on the other samples in its batch.
2. Layer norm averages across the features of a single sample. It behaves the same at batch size 1 and at inference.
3. Both then apply a learnable scale γ and shift β.

```python
import numpy as np
rng = np.random.default_rng(12)
X = rng.normal(5, 3, size=(4, 6))                  # batch of 4 samples, 6 features
eps = 1e-5
ln = (X - X.mean(1, keepdims=True)) / np.sqrt(X.var(1, keepdims=True) + eps)   # per sample
bn = (X - X.mean(0, keepdims=True)) / np.sqrt(X.var(0, keepdims=True) + eps)   # per feature
print("LayerNorm  row means:", ln.mean(1).round(6), " row stds:", ln.std(1).round(3))
print("BatchNorm  col means:", bn.mean(0).round(6))
ln_single = (X[:1] - X[:1].mean()) / np.sqrt(X[:1].var() + eps)
print("LN of sample 0 alone equals LN in batch:", np.allclose(ln_single, ln[:1]))
```

Output:

```
LayerNorm  row means: [ 0.  0. -0.  0.]  row stds: [1. 1. 1. 1.]
BatchNorm  col means: [-0. -0. -0.  0. -0.  0.]
LN of sample 0 alone equals LN in batch: True
```

### A feed-forward layer as key-value memory

1. FFN(x) = f(x·Kᵀ)·V. Each row of K is a key (a pattern detector), and each row of V is the value it writes out.
2. The activation f(x·k_i) says how strongly memory i fires, so the output is a weighted sum of value vectors.
3. To edit a fact (as ROME and MEMIT do), change V so that the key for a subject maps to a new value. Other keys are left alone, which is the specificity requirement.

```python
import numpy as np
rng = np.random.default_rng(13)
d, m = 16, 4                                   # 4 memories
K = 3 * np.linalg.qr(rng.normal(size=(d, m)))[0].T   # 4 nearly independent keys
V = rng.normal(size=(m, d))
relu = lambda a: np.maximum(a, 0)

x = K[2] + 0.1 * rng.normal(size=d)            # input that matches key 2
coef = relu(x @ K.T)
print("memory activations:", coef.round(2))
print("output is mostly value 2:", np.corrcoef(coef @ V, V[2])[0, 1].round(3))

new_value = rng.normal(size=d)                 # "edit" memory 2 only
V2 = V.copy(); V2[2] = new_value
print("after edit, output tracks new value:", np.corrcoef(relu(x @ K.T) @ V2, new_value)[0, 1].round(3))
```

Output:

```
memory activations: [0.15 0.01 8.87 0.32]
output is mostly value 2: 0.999
after edit, output tracks new value: 0.999
```

### Causal mediation: total, direct and indirect effects

1. Toy network: input x → mediator m = tanh(2x) → output y = 3m + 0.5x.
2. Total effect: change x and let everything update. Direct effect: change x but clamp m at its old value. Indirect effect: keep x and set m to the value it would take under the new x.
3. Here most of the effect flows through m, so the mediator matters. Causal tracing in LLMs applies this idea to hidden states.

```python
import numpy as np
m_of = lambda x: np.tanh(2 * x)
y_of = lambda x, m: 3 * m + 0.5 * x
x0, x1 = 0.0, 0.5
total    = y_of(x1, m_of(x1)) - y_of(x0, m_of(x0))
direct   = y_of(x1, m_of(x0)) - y_of(x0, m_of(x0))   # vary x, clamp mediator
indirect = y_of(x0, m_of(x1)) - y_of(x0, m_of(x0))   # keep x, move mediator
print(f"total={total:.3f} direct={direct:.3f} indirect={indirect:.3f}")
```

Output:

```
total=2.535 direct=0.250 indirect=2.285
```

## Class 5 · Autoregressive Models

### Autoregressive likelihood is exact (chain rule)

1. Any joint distribution factorizes as p(x_1..x_T) = ∏_t p(x_t | x_<t). No approximation is involved.
2. So log p(x) is just the sum of per-step log-probabilities. Below we use a tiny bigram model: it is a proper distribution, and the total probability approaches 1 as longer sequences are included.
3. Generation must go one step at a time, because each step needs the previous output.

```python
import numpy as np, itertools
vocab = ["a", "b", "<eos>"]
start = np.array([0.6, 0.4, 0.0])
trans = np.array([[0.1, 0.6, 0.3], [0.5, 0.2, 0.3], [0, 0, 1]])   # p(next | prev)

def log_p(seq):
    idx = [vocab.index(s) for s in seq]
    return np.log(start[idx[0]]) + sum(np.log(trans[a, b]) for a, b in zip(idx, idx[1:]))

print("log p(a b a <eos>) =", log_p(["a", "b", "a", "<eos>"]).round(4))
for maxlen in (4, 10, 16):          # brute-force: every sequence that ends in <eos>
    total = sum(np.exp(log_p(list(s) + ["<eos>"]))
                for L in range(1, maxlen + 1) for s in itertools.product("ab", repeat=L))
    print(f"total probability of all sequences up to length {maxlen:2d}: {total:.6f}")
```

Output:

```
log p(a b a <eos>) = -2.9188
total probability of all sequences up to length  4: 0.759900
total probability of all sequences up to length 10: 0.971752
total probability of all sequences up to length 16: 0.996677
```

### BPTT: products of Jacobians vanish

1. h_t = tanh(W h_{t−1} + U x_t). Then ∂h_T/∂h_t = ∏ diag(1 − h²)·W, one factor per step.
2. Because W is shared, BPTT sums gradient contributions from every step. Each long-range term is still a long product, though.
3. With ‖W‖ < 1 and tanh’ ≤ 1 the product decays geometrically, so distant steps contribute almost nothing.

```python
import numpy as np
rng = np.random.default_rng(14)
d = 32
W = rng.normal(0, 0.9 / np.sqrt(d), (d, d)); U = rng.normal(0, 1, (d, d))
h, hs = np.zeros(d), []
for t in range(60):
    h = np.tanh(W @ h + U @ rng.normal(size=d) * 0.3); hs.append(h)

J = np.eye(d)                                  # d h_T / d h_t, accumulated backward
for t in range(59, -1, -1):
    if t in (59, 49, 39, 19, 0):
        print(f"steps back = {59 - t:2d}   ||dh_T/dh_t|| = {np.linalg.norm(J, 2):.2e}")
    J = J @ (np.diag(1 - hs[t]**2) @ W)
```

Output:

```
steps back =  0   ||dh_T/dh_t|| = 1.00e+00
steps back = 10   ||dh_T/dh_t|| = 2.79e-03
steps back = 20   ||dh_T/dh_t|| = 1.17e-06
steps back = 40   ||dh_T/dh_t|| = 2.32e-13
steps back = 59   ||dh_T/dh_t|| = 6.42e-20
```

### One LSTM step: gates and the cell’s linear self-loop

1. Gates f, i, o are sigmoids in (0, 1). The candidate g uses tanh.
2. The cell update c_t = f ⊙ c_{t−1} + i ⊙ g is additive. The gradient through c is multiplied by f, not by a squashing derivative.
3. With f ≈ 1 and i ≈ 0, the cell carries information unchanged across many steps. That is how LSTMs bridge long gaps.

```python
import numpy as np
sig = lambda a: 1 / (1 + np.exp(-a))
def lstm_step(x, h, c, P):
    z = P["W"] @ np.r_[x, h] + P["b"]
    f, i, o, g = np.split(z, 4)
    f, i, o, g = sig(f), sig(i), sig(o), np.tanh(g)
    c = f * c + i * g                 # linear self-loop, gated by f
    return o * np.tanh(c), c

rng = np.random.default_rng(15); d = 4
P = {"W": rng.normal(0, 0.1, (4 * d, 2 * d)), "b": np.r_[np.full(d, 6.), np.full(d, -6.), np.zeros(2 * d)]}
c = np.array([1.0, -0.5, 0.8, 0.2]); h = np.zeros(d)   # bias: forget=+6 (open), input=-6 (closed)
c0 = c.copy()
for _ in range(100):
    h, c = lstm_step(rng.normal(size=d), h, c, P)
print("cell state at t=0  :", c0)
print("cell state at t=100:", c.round(3))
```

Output:

```
cell state at t=0  : [ 1.  -0.5  0.8  0.2]
cell state at t=100: [ 0.78 -0.41  0.62  0.16]
```

### One GRU step: update and reset gates

1. Reset r chooses how much of h_{t−1} feeds the candidate h̃ = tanh(W x + U(r ⊙ h_{t−1})). With r ≈ 0 the candidate ignores the past.
2. Update u blends old and new: h_t = u ⊙ h_{t−1} + (1 − u) ⊙ h̃ (Goodfellow’s convention). With u ≈ 1 the state is copied forward.
3. Two gates do the job of the LSTM’s three, with no separate cell state.

```python
import numpy as np
sig = lambda a: 1 / (1 + np.exp(-a))
rng = np.random.default_rng(16); d = 3
W, U = rng.normal(size=(d, d)), rng.normal(size=(d, d))
x, h_prev = rng.normal(size=d), np.array([0.9, -0.7, 0.4])

def gru(u_val, r_val):
    u, r = np.full(d, u_val), np.full(d, r_val)
    cand = np.tanh(W @ x + U @ (r * h_prev))
    return u * h_prev + (1 - u) * cand, cand

for u_val, r_val in [(0.999, 0.5), (0.001, 0.0), (0.001, 1.0)]:
    h, cand = gru(u_val, r_val)
    print(f"u={u_val:<5} r={r_val}:  h_t={h.round(3)}")
print("h_prev =", h_prev)
```

Output:

```
u=0.999 r=0.5:  h_t=[ 0.9 -0.7  0.4]
u=0.001 r=0.0:  h_t=[0.17 0.43 0.65]
u=0.001 r=1.0:  h_t=[-0.73 -0.27  0.75]
h_prev = [ 0.9 -0.7  0.4]
```

### PixelCNN masks A and B

1. Order pixels in raster scan (row by row, left to right). A pixel may only see pixels above it, or to its left in the same row.
2. Mask A (first layer) also hides the center, so a pixel never sees its own value.
3. Mask B (later layers) shows the center, because after layer 1 the center feature already summarizes only earlier pixels.

```python
import numpy as np
def mask(k, kind):
    m = np.ones((k, k), dtype=int); c = k // 2
    m[c, c + (kind == "B"):] = 0      # center row: block center (A) or only right of it (B)
    m[c + 1:, :] = 0                  # block all rows below
    return m
print("Mask A (5x5):\n", mask(5, "A"))
print("Mask B (5x5):\n", mask(5, "B"))
```

Output:

```
Mask A (5x5):
 [[1 1 1 1 1]
 [1 1 1 1 1]
 [1 1 0 0 0]
 [0 0 0 0 0]
 [0 0 0 0 0]]
Mask B (5x5):
 [[1 1 1 1 1]
 [1 1 1 1 1]
 [1 1 1 0 0]
 [0 0 0 0 0]
 [0 0 0 0 0]]
```

## Class 6 · Multimodal LLMs

### Byte Pair Encoding, a few merges

1. Start with characters as symbols. Count every adjacent pair across the corpus (weighted by word frequency).
2. Merge the most frequent pair into a new symbol, and repeat.
3. Frequent subwords such as ‘est’ or ‘low’ become single tokens, while rare words stay split into pieces. No word is ever out of vocabulary.

```python
from collections import Counter
corpus = {"low": 5, "lower": 2, "newest": 6, "widest": 3}
words = {tuple(w) + ("</w>",): f for w, f in corpus.items()}

for step in range(1, 6):
    pairs = Counter()
    for w, f in words.items():
        for a, b in zip(w, w[1:]):
            pairs[a, b] += f
    (a, b), cnt = pairs.most_common(1)[0]
    new = {}
    for w, f in words.items():
        out, i = [], 0
        while i < len(w):
            if i < len(w) - 1 and (w[i], w[i + 1]) == (a, b):
                out.append(a + b); i += 2
            else:
                out.append(w[i]); i += 1
        new[tuple(out)] = f
    words = new
    print(f"merge {step}: '{a}'+'{b}' (count {cnt}) -> {list(words)}")
```

Output:

```
merge 1: 'e'+'s' (count 9) -> [('l', 'o', 'w', '</w>'), ('l', 'o', 'w', 'e', 'r', '</w>'), ('n', 'e', 'w', 'es', 't', '</w>'), ('w', 'i', 'd', 'es', 't', '</w>')]
merge 2: 'es'+'t' (count 9) -> [('l', 'o', 'w', '</w>'), ('l', 'o', 'w', 'e', 'r', '</w>'), ('n', 'e', 'w', 'est', '</w>'), ('w', 'i', 'd', 'est', '</w>')]
merge 3: 'est'+'</w>' (count 9) -> [('l', 'o', 'w', '</w>'), ('l', 'o', 'w', 'e', 'r', '</w>'), ('n', 'e', 'w', 'est</w>'), ('w', 'i', 'd', 'est</w>')]
merge 4: 'l'+'o' (count 7) -> [('lo', 'w', '</w>'), ('lo', 'w', 'e', 'r', '</w>'), ('n', 'e', 'w', 'est</w>'), ('w', 'i', 'd', 'est</w>')]
merge 5: 'lo'+'w' (count 7) -> [('low', '</w>'), ('low', 'e', 'r', '</w>'), ('n', 'e', 'w', 'est</w>'), ('w', 'i', 'd', 'est</w>')]
```

### ViT patchify: an image becomes 197 tokens

1. A 224×224×3 image is cut into 16×16 patches, giving (224/16)² = 196 patches of 16·16·3 = 768 values each.
2. A linear projection maps each patch to d_model. A learnable [class] token is prepended, so there are 197 tokens.
3. A learnable position embedding of shape (197, d_model) is added. After that it is a plain Transformer encoder.

```python
import numpy as np
rng = np.random.default_rng(17)
img = rng.random((224, 224, 3)); P, d_model = 16, 768
patches = img.reshape(224 // P, P, 224 // P, P, 3).transpose(0, 2, 1, 3, 4).reshape(-1, P * P * 3)
E = rng.normal(0, 0.02, (P * P * 3, d_model))
tokens = patches @ E
cls = np.zeros((1, d_model)); pos = rng.normal(0, 0.02, (197, d_model))
seq = np.vstack([cls, tokens]) + pos
print("patches:", patches.shape, "-> tokens:", tokens.shape, "-> with [class] + pos:", seq.shape)
```

Output:

```
patches: (196, 768) -> tokens: (196, 768) -> with [class] + pos: (197, 768)
```

### CLIP: symmetric contrastive loss and zero-shot classification

1. In a batch of N matched pairs, the N×N cosine-similarity matrix should have its large values on the diagonal.
2. The loss is cross-entropy over rows (image→text) plus cross-entropy over columns (text→image), averaged.
3. Zero-shot: embed ‘a photo of a {class}’ for each class and pick the class whose text embedding is most similar to the image.

```python
import numpy as np
rng = np.random.default_rng(18)
def norm(a): return a / np.linalg.norm(a, axis=1, keepdims=True)
def xent_diag(L):                       # cross-entropy with targets on the diagonal
    L = L - L.max(1, keepdims=True)
    return -np.mean(np.diag(L) - np.log(np.exp(L).sum(1)))

N, d, temp = 6, 32, 0.07
concepts = rng.normal(size=(N, d))
img = norm(concepts + 0.3 * rng.normal(size=(N, d)))
txt = norm(concepts + 0.3 * rng.normal(size=(N, d)))
logits = img @ txt.T / temp
print("symmetric loss, matched pairs :", ((xent_diag(logits) + xent_diag(logits.T)) / 2).round(4))
shuffled = img @ txt[rng.permutation(N)].T / temp
print("symmetric loss, shuffled pairs:", ((xent_diag(shuffled) + xent_diag(shuffled.T)) / 2).round(4))

classes = ["dog", "cat", "car", "tree", "boat", "lamp"]   # zero-shot with "text prompts"
query = norm(concepts[[3]] + 0.3 * rng.normal(size=(1, d)))
print("zero-shot prediction:", classes[int(np.argmax(query @ txt.T))])
```

Output:

```
symmetric loss, matched pairs : 0.0014
symmetric loss, shuffled pairs: 8.4391
zero-shot prediction: tree
```

### Flamingo’s tanh gate and the Perceiver Resampler

1. A new cross-attention block adds tanh(α)·xattn(y, visual) to the frozen LM’s residual stream y.
2. With α = 0, tanh(0) = 0, so the model is exactly the pretrained LM at initialization. Training then opens the gate gradually.
3. The resampler compresses any number of visual features to 64 latent tokens, so text-to-vision cross-attention costs n_text × 64 instead of n_text × n_visual.

```python
import numpy as np
rng = np.random.default_rng(19)
y = rng.normal(size=(10, 16))                     # frozen LM hidden states (10 text tokens)
xattn = rng.normal(size=(10, 16))                 # output of new cross-attention block
for alpha in (0.0, 0.5, 2.0):
    out = y + np.tanh(alpha) * xattn
    print(f"alpha={alpha}: change to LM stream = {np.abs(out - y).max():.3f}")

n_text, n_vis, n_lat = 512, 5 * 8 * 8 * 30, 64     # e.g. 5 images x 30 frames x 8x8 grid
print("cross-attn scores without resampler:", n_text * n_vis, "| with 64 latents:", n_text * n_lat)
```

Output:

```
alpha=0.0: change to LM stream = 0.000
alpha=0.5: change to LM stream = 1.302
alpha=2.0: change to LM stream = 2.717
cross-attn scores without resampler: 4915200 | with 64 latents: 32768
```

## Class 7 · Diffusion Models

### Forward diffusion keeps variance at 1 and erases the signal

1. z_t = √(1−β)·z_{t−1} + √β·ε. If Var(z_{t−1}) = 1, then Var(z_t) = (1−β) + β = 1.
2. The signal is attenuated by √(1−β) each step, so the correlation with x decays like √ᾱ_t, where ᾱ_t = ∏(1−β).
3. After enough steps, every starting point ends up distributed as N(0, 1), regardless of x.

```python
import numpy as np
rng = np.random.default_rng(20)
x = rng.choice([-1.5, 0.5, 1.8], size=50_000) + 0.1 * rng.standard_normal(50_000)
x = (x - x.mean()) / x.std()                      # normalize data to unit variance
beta, z = 0.03, x.copy()
for t in range(1, 101):
    z = np.sqrt(1 - beta) * z + np.sqrt(beta) * rng.standard_normal(z.shape)
    if t in (1, 10, 50, 100):
        abar = (1 - beta) ** t
        print(f"t={t:3d}  var={z.var():.3f}  corr(x,z)={np.corrcoef(x, z)[0,1]:.3f}  sqrt(abar)={np.sqrt(abar):.3f}")
```

Output:

```
t=  1  var=1.002  corr(x,z)=0.985  sqrt(abar)=0.985
t= 10  var=1.009  corr(x,z)=0.859  sqrt(abar)=0.859
t= 50  var=0.991  corr(x,z)=0.468  sqrt(abar)=0.467
t=100  var=0.991  corr(x,z)=0.219  sqrt(abar)=0.218
```

### The diffusion kernel: jump to step t in one shot

1. Composing t Gaussian steps gives one Gaussian: q(z_t | x) = N(√ᾱ_t·x, (1−ᾱ_t)·I), with ᾱ_t = ∏_{s≤t}(1−β_s).
2. Training samples a random t and sets z_t = √ᾱ_t·x + √(1−ᾱ_t)·ε directly. No loop is needed.
3. That same ε is the regression target: the network learns ε̂(z_t, t) ≈ ε.

```python
import numpy as np
rng = np.random.default_rng(21)
T = 1000; betas = np.linspace(1e-4, 0.02, T); abar = np.cumprod(1 - betas)
x, t = 1.7, 300

z = np.full(200_000, x)                           # iterate step by step
for s in range(t):
    z = np.sqrt(1 - betas[s]) * z + np.sqrt(betas[s]) * rng.standard_normal(z.shape)
eps = rng.standard_normal(200_000)
z_direct = np.sqrt(abar[t - 1]) * x + np.sqrt(1 - abar[t - 1]) * eps   # one shot

print(f"iterated: mean={z.mean():.4f} var={z.var():.4f}")
print(f"kernel  : mean={z_direct.mean():.4f} var={z_direct.var():.4f}")
print(f"formula : mean={np.sqrt(abar[t-1]) * x:.4f} var={1 - abar[t-1]:.4f}")
```

Output:

```
iterated: mean=1.0715 var=0.6058
kernel  : mean=1.0680 var=0.6027
formula : mean=1.0704 var=0.6036
```

### Linear vs cosine noise schedules

1. Linear β from 1e-4 to 0.02 destroys signal quickly in the middle. ᾱ_t is near 0 well before t = T, so the last steps are wasted on pure noise.
2. The cosine schedule defines ᾱ_t = cos²((t/T + s)/(1 + s) · π/2) directly, which spreads signal loss more evenly over t.
3. Compare √ᾱ_t, the remaining signal rate, at the same fractions of T.

```python
import numpy as np
T = 1000; t = np.array([100, 250, 500, 750, 900])
abar_lin = np.cumprod(1 - np.linspace(1e-4, 0.02, T))[t - 1]
s = 0.008
f = lambda u: np.cos((u / T + s) / (1 + s) * np.pi / 2) ** 2
abar_cos = f(t) / f(0)
for ti, a, b in zip(t, abar_lin, abar_cos):
    print(f"t={ti:4d}  signal rate linear={np.sqrt(a):.3f}  cosine={np.sqrt(b):.3f}")
```

Output:

```
t= 100  signal rate linear=0.947  cosine=0.986
t= 250  signal rate linear=0.724  cosine=0.920
t= 500  signal rate linear=0.280  cosine=0.703
t= 750  signal rate linear=0.058  cosine=0.380
t= 900  signal rate linear=0.017  cosine=0.155
```

### q(z_{t−1} | z_t, x): the exact reverse step given x

1. Bayes’ rule: q(z_{t−1} | z_t, x) ∝ q(z_t | z_{t−1}) · q(z_{t−1} | x). Both factors are Gaussian, so the product is Gaussian.
2. Its mean is a weighted blend of x and z_t, and its variance β̃_t = β_t(1−ᾱ_{t−1})/(1−ᾱ_t) is smaller than β_t.
3. We verify the closed form by brute force: simulate (z_{t−1}, z_t) pairs and regress.

```python
import numpy as np
rng = np.random.default_rng(22)
T = 1000; betas = np.linspace(1e-4, 0.02, T); abar = np.cumprod(1 - betas)
t, x = 400, 0.8
b, a_t, a_prev = betas[t - 1], abar[t - 1], abar[t - 2]
c_x = np.sqrt(a_prev) * b / (1 - a_t)
c_z = np.sqrt(1 - b) * (1 - a_prev) / (1 - a_t)
var = b * (1 - a_prev) / (1 - a_t)

zp = np.sqrt(a_prev) * x + np.sqrt(1 - a_prev) * rng.standard_normal(400_000)   # z_{t-1} | x
zt = np.sqrt(1 - b) * zp + np.sqrt(b) * rng.standard_normal(zp.shape)           # z_t | z_{t-1}
slope, icpt = np.polyfit(zt, zp, 1)
resid = zp - (slope * zt + icpt)
print(f"closed form: mean = {c_z:.4f}*z_t + {c_x * x:.4f}, var = {var:.6f}")
print(f"simulation : mean = {slope:.4f}*z_t + {icpt:.4f}, var = {resid.var():.6f}")
```

Output:

```
closed form: mean = 0.9940*z_t + 0.0035, var = 0.008032
simulation : mean = 0.9940*z_t + 0.0034, var = 0.008043
```

### A DDIM step: estimate x₀, then re-noise to t−1

1. From z_t = √ᾱ_t·x₀ + √(1−ᾱ_t)·ε, a noise prediction ε̂ gives x̂₀ = (z_t − √(1−ᾱ_t)·ε̂)/√ᾱ_t.
2. Deterministic DDIM (σ = 0): z_{t−1} = √ᾱ_{t−1}·x̂₀ + √(1−ᾱ_{t−1})·ε̂. You can jump between any two noise levels, so 20 steps can replace 1,000.
3. With a perfect ε̂ the trajectory lands exactly on x₀. With the same starting noise, the result is always the same.

```python
import numpy as np
rng = np.random.default_rng(23)
T = 1000; abar = np.cumprod(1 - np.linspace(1e-4, 0.02, T))
x0 = np.array([0.5, -1.2, 2.0])
eps = rng.standard_normal(3)
steps = np.linspace(T - 1, 0, 20).astype(int)          # 20 of the 1,000 levels
z = np.sqrt(abar[steps[0]]) * x0 + np.sqrt(1 - abar[steps[0]]) * eps

oracle = lambda z, t: (z - np.sqrt(abar[t]) * x0) / np.sqrt(1 - abar[t])   # a perfect noise predictor
for t, t_prev in zip(steps[:-1], steps[1:]):
    e = oracle(z, t)
    x0_hat = (z - np.sqrt(1 - abar[t]) * e) / np.sqrt(abar[t])
    z = np.sqrt(abar[t_prev]) * x0_hat + np.sqrt(1 - abar[t_prev]) * e
print("start noise level t =", steps[0], "| steps taken:", len(steps) - 1)
print("recovered x0:", np.round((z - np.sqrt(1 - abar[0]) * oracle(z, 0)) / np.sqrt(abar[0]), 4), "| true:", x0)
```

Output:

```
start noise level t = 999 | steps taken: 19
recovered x0: [ 0.5 -1.2  2. ] | true: [ 0.5 -1.2  2. ]
```

### Linear vs spherical interpolation of Gaussian noise

1. For independent unit-variance a and b, the linear midpoint (a + b)/2 has variance 1/4 + 1/4 = 1/2. That is not what the denoiser was trained on.
2. Spherical interpolation uses weights sin(θ) and cos(θ). The variance is sin² + cos² = 1 at every θ.
3. So every interpolant is still valid N(0, I) noise, and deterministic DDIM decoding gives smooth image transitions.

```python
import numpy as np
rng = np.random.default_rng(24)
a, b = rng.standard_normal((2, 100_000))
for s in (0.0, 0.25, 0.5):
    lin = (1 - s) * a + s * b
    th = s * np.pi / 2
    sph = np.cos(th) * a + np.sin(th) * b
    print(f"s={s:4}: var linear={lin.var():.3f}   var spherical={sph.var():.3f}")
```

Output:

```
s= 0.0: var linear=1.004   var spherical=1.004
s=0.25: var linear=0.626   var spherical=1.001
s= 0.5: var linear=0.500   var spherical=1.001
```

### Classifier-free guidance arithmetic

1. Train one network both with and without the condition c (c is dropped at random during training).
2. At sampling: ε̃ = ε(z, ∅) + w·(ε(z, c) − ε(z, ∅)). w = 1 is plain conditional, w > 1 pushes harder toward c.
3. Larger w gives samples that match c more strongly (quality and fidelity) but are less varied (diversity). That is the trade-off knob.

```python
import numpy as np
eps_uncond = np.array([0.2, -0.1, 0.4])
eps_cond   = np.array([0.5, -0.3, 0.1])
for w in (0.0, 1.0, 3.0, 7.5):
    print(f"w={w:<4} guided eps = {(eps_uncond + w * (eps_cond - eps_uncond)).round(2)}")
```

Output:

```
w=0.0  guided eps = [ 0.2 -0.1  0.4]
w=1.0  guided eps = [ 0.5 -0.3  0.1]
w=3.0  guided eps = [ 1.1 -0.7 -0.5]
w=7.5  guided eps = [ 2.45 -1.6  -1.85]
```
