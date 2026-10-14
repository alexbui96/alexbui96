# SEAS 8525 Generative AI Question Bank

265 questions from Classes 1–7 and the SimCLR paper.

- ○ = single answer (exactly one correct)
- ☐ = select all that apply (two or more correct)

The answer key and explanations for each class follow its questions, so you can quiz yourself first.

---

## Class 1 · Introduction to Generative AI

**Q1.** ○ *Single answer.* A model is trained to estimate p(y | x), where x is a painting and y ∈ {Van Gogh, not Van Gogh}. Which statement best characterizes what this model can and cannot do?

- ○ **A.** It can output the probability that a new painting is a Van Gogh, but it has no mechanism for producing a new Van Gogh-like painting
- ○ **B.** It can generate new Van Gogh paintings by sampling from p(y | x) with a high temperature
- ○ **C.** It is equivalent to a conditional generative model p(x | y) once training converges, because Bayes’ rule lets us invert any classifier
- ○ **D.** It is a generative model because it was trained on images

**Q2.** ☐ *Select all that apply.* Which properties are required for a model to count as a true generative model? Select all that apply.

- ☐ **A.** It must use labeled data so that each generated sample has a known class
- ☐ **B.** It must be a fixed computation, such as averaging the pixel values of the training images, so the output is reproducible
- ☐ **C.** It must be probabilistic, with a random component, so it can produce varied outputs
- ☐ **D.** It must be able to generate novel observations that look like they were drawn from p_data

**Q3.** ○ *Single answer.* In the world-map “Hello World” example, the model family is the set of uniform distributions over axis-aligned boxes. How many parameters does each density p_θ in this parametric family have, and what are they?

- ○ **A.** Two: the center of the box (x, y), since uniform densities have no shape parameters
- ○ **B.** Three: the center coordinate pair plus a single side length shared by all four edges
- ○ **C.** Infinitely many, because a density function is defined at every point in the continuous sample space
- ○ **D.** Four: the bottom-left (θ1, θ2) and top-right (θ3, θ4) corners

**Q4.** ○ *Single answer.* A candidate box covers only the left half of the world map, but the observed dataset X contains points in the right half. What is the likelihood L(θ | X) of this box, and why?

- ○ **A.** Small but positive, because the likelihood averages the per-point densities over all of the observed points in X
- ○ **B.** Exactly 0.5, since half of the map is covered
- ○ **C.** Zero, since one observed point has density 0 and the likelihood is a product
- ○ **D.** Undefined, because the log-likelihood of zero is −∞, so likelihood cannot be computed

**Q5.** ○ *Single answer.* Why do we usually maximize the log-likelihood ℓ(θ|X) = Σ log p_θ(x_i) rather than the likelihood ∏ p_θ(x_i) directly?

- ○ **A.** The log-likelihood is always convex in θ for neural networks, so gradient descent is guaranteed to find the global optimum
- ○ **B.** Products of many values in (0, 1) underflow; a sum of logs is stable and has the same maximizer
- ○ **C.** Probabilities greater than 1 cannot be represented
- ○ **D.** The log shifts the location of the maximum toward regions of higher probability mass, which yields a less biased estimate

**Q6.** ☐ *Select all that apply.* Match the taxonomy of generative models presented in Class 1. Which pairings are correct? Select all that apply.

- ☐ **A.** Implicit density: GANs, which learn a stochastic process that generates data without estimating a density
- ☐ **B.** Approximate explicit density: VAEs, energy-based models and diffusion models
- ☐ **C.** Tractable explicit density: autoregressive models and normalizing flows
- ☐ **D.** Implicit density: VAEs, because they sample a latent vector before decoding
- ☐ **E.** Tractable explicit density: diffusion models, because their forward noising process has a closed-form kernel

**Q7.** ○ *Single answer.* A conditional generative model is trained on a fruit dataset so that we can ask it specifically for an apple. Which quantity does it estimate?

- ○ **A.** p(y), the class prior, i.e., how often each fruit label appears in the training data
- ○ **B.** p(y | x), the probability of the label given the image
- ○ **C.** p(x) only, since a label cannot influence a generative model once it has been trained
- ○ **D.** p(x | y), the probability of an observation given a label

**Q8.** ○ *Single answer.* A dataset of biscuit-tin photos varies in only two ways: height and width. What is the core idea of representation learning in this setting?

- ○ **A.** Hand-code the important features (e.g., height, width) so the machine does not need to learn them
- ○ **B.** Encode data into a low-dimensional latent space and learn a mapping from latent points back to data
- ○ **C.** Increase the dimensionality of the data so that the classes become linearly separable for a downstream discriminator
- ○ **D.** Store every training image in a lookup table and retrieve the nearest one at generation time

**Q9.** ☐ *Select all that apply.* Why is generative modeling of high-dimensional data hard? Select all that apply.

- ☐ **A.** The sample space is discrete, so densities cannot be defined
- ☐ **B.** Explicitly modeling the full dimensionality, i.e., computing p_θ(x) directly, is generally intractable
- ☐ **C.** Discriminative models already solve the problem, so there is little demand for better generative models from industry or research
- ☐ **D.** Training data covers only a sparse subset of the possible observations
- ☐ **E.** The true distribution lives in an exponentially high-dimensional space

**Q10.** ○ *Single answer.* Which three properties make a generative model p_model useful?

- ○ **A.** Determinism, reproducibility, and explainability, since outputs should be identical across runs
- ○ **B.** Speed, memory efficiency, and differentiability
- ○ **C.** Convexity, sparsity, and calibration
- ○ **D.** Accuracy, generation, and representation

**Q11.** ○ *Single answer.* Which ordering of the Generative AI project life cycle is correct?

- ○ **A.** Identify use case → Experiment & select → Adapt & augment → Evaluate → Deploy → Monitor
- ○ **B.** Experiment & select → Identify use case → Deploy & integrate → Adapt & augment → Monitor → Evaluate
- ○ **C.** Collect data → Train a new model from scratch → Evaluate on a held-out set → Deploy
- ○ **D.** Identify use case → Deploy the base model → Fine-tune on production logs → Monitor drift

**Q12.** ☐ *Select all that apply.* The healthcare and military ethics comparison (Oniani et al., 2023) identified shared core principles. Which of the following are shared principles? Select all that apply.

- ☐ **A.** Profitability
- ☐ **B.** Governability
- ☐ **C.** Traceability
- ☐ **D.** Equity
- ☐ **E.** Maximum autonomy without human oversight

**Q13.** ○ *Single answer.* In Dual Diffusion Implicit Bridges (DDIBs) for image-to-image translation (e.g., tiger → cat), how is the translation achieved?

- ○ **A.** The source ODE runs forward to a shared latent; the target model’s ODE runs in reverse from it
- ○ **B.** A single diffusion model is fine-tuned on both domains simultaneously with an added cycle-consistency loss between them
- ○ **C.** The latent vector of the source image is decoded directly by a VAE decoder trained on the target domain
- ○ **D.** A GAN discriminator is trained on paired tiger–cat images

**Q14.** ○ *Single answer.* Reinforcement learning differs from supervised and unsupervised learning in that it

- ○ **A.** uses only dimensionality reduction to compress the state space before predicting labels
- ○ **B.** learns a series of actions in a decision process driven by rewards
- ○ **C.** uses labeled data with direct, immediate feedback on every single input it receives
- ○ **D.** finds hidden structure in unlabeled data without any feedback

**Q15.** ○ *Single answer.* “There is only one true density p_data, but infinitely many densities p_model we could use to estimate it.” What is the role of parametric modeling given this fact?

- ○ **A.** It forces the model to be non-probabilistic
- ○ **B.** It eliminates the need for a likelihood function, since densities can be compared visually
- ○ **C.** It guarantees that p_model = p_data exactly once enough independent observations have been collected from the true distribution
- ○ **D.** It restricts the search to a family p_θ with finitely many parameters, turning estimation into optimization over θ

**Q16.** ○ *Single answer.* Which family is an example of an approximate explicit density model that uses Markov-chain sampling rather than variational methods?

- ○ **A.** Energy-based models
- ○ **B.** Autoregressive models such as PixelCNN
- ○ **C.** Normalizing flows
- ○ **D.** Generative adversarial networks, whose generator is trained through a separate discriminator network

**Q17.** ○ *Single answer.* A normalizing flow keeps its density tractable by

- ○ **A.** applying a chain of invertible, tractable transformations to a simple base distribution
- ○ **B.** training a discriminator to score samples and backpropagating its judgment into a generator network
- ○ **C.** bounding the likelihood with an ELBO
- ○ **D.** imposing an ordering on input features and generating them one at a time

**Q18.** ☐ *Select all that apply.* In the sample-space example on the world map, which statements are correct? Select all that apply.

- ☐ **A.** The sample space is all (latitude, longitude) points x = (x1, x2)
- ☐ **B.** New York City (40.7306, −73.9352) lies inside the true data-generating distribution
- ☐ **C.** The point (11.3493, 142.1996) is in the sample space but not in the true distribution, because it is at sea
- ☐ **D.** Points at sea are outside the sample space, since the sample space is defined as only the observed points in X

**Q19.** ○ *Single answer.* Which statement about a probability density function is required for it to be a well-defined distribution?

- ○ **A.** It must be differentiable everywhere
- ○ **B.** Its maximum value must be at most 1
- ○ **C.** Its integral over the whole sample space equals 1
- ○ **D.** It must be symmetric about its mean, as a Gaussian is, so that probabilities are balanced on both sides

**Q20.** ☐ *Select all that apply.* Which of the following are unsupervised learning techniques mentioned in Class 1? Select all that apply.

- ☐ **A.** Logistic regression trained on pass/fail labels so that it can predict the outcome for new students
- ☐ **B.** Dimensionality reduction, e.g., projecting 3-D data to 2-D
- ☐ **C.** Clustering, e.g., grouping elephants and zebras without labels
- ☐ **D.** Generative modeling, which learns to produce new data similar to the training set

**Q21.** ○ *Single answer.* Why did industry historically favor discriminative models over generative ones?

- ○ **A.** They were easier to apply to practical tasks, e.g., doctors wanted diagnoses, not new images
- ○ **B.** Generative models were illegal to deploy
- ○ **C.** Discriminative models need no training data, while every generative model needs millions of labeled examples
- ○ **D.** Generative models cannot run on GPUs

**Q22.** ○ *Single answer.* What does this function return for a box that leaves one data point outside it, and why?

```python
def log_lik(box, X):
    x1, y1, x2, y2 = box
    inside = (X[:,0] >= x1) & (X[:,0] <= x2) & (X[:,1] >= y1) & (X[:,1] <= y2)
    if not inside.all():
        return -np.inf
    return len(X) * np.log(1 / ((x2 - x1) * (y2 - y1)))
```

- ○ **A.** A small negative number proportional to how far outside the box the stray point lies
- ○ **B.** NaN, because the area is undefined
- ○ **C.** 0, because log(0) is clipped to zero
- ○ **D.** −inf: one point has density 0, so the product of densities is 0

**Q23.** ○ *Single answer.* What does this code demonstrate?

```python
p = rng.uniform(0.01, 0.5, size=1000)
print(np.prod(p))            # ?
print(np.sum(np.log(p)))     # ?
```

- ○ **A.** It raises a NumPy overflow error
- ○ **B.** The product is more accurate than the sum
- ○ **C.** Logarithms change which parameters maximize the likelihood, so the two results disagree on the best fit
- ○ **D.** np.prod(p) underflows to 0.0, while the sum of logs is about −1600 and usable


### Answer key — Class 1 · Introduction to Generative AI

**Q1 → A**

Discriminative (conditional) models such as logistic regression, CRFs and decision trees model p(y|x) directly and learn decision boundaries. Generative models model p(x), or p(x|y) when conditional, and sampling from that distribution is what produces new observations. Concretely, a classifier is a function f(x) → [0, 1]. To produce a painting you would have to search or optimize over x, and its output says nothing about which x are realistic. See the code below: the generative model can both classify (via Bayes) and sample.

- A: ✓ Correct. A discriminative model only learns the conditional p(y|x); it never models how x itself is distributed, so it cannot sample new x.
- B: ✗ Sampling from p(y|x) yields labels, not images. Temperature does not change what space you sample in.
- C: ✗ Inverting with Bayes needs p(x|y) = p(y|x)p(x)/p(y), and the classifier never learned p(x). Without p(x) there is nothing to sample from.
- D: ✗ Training on images does not make a model generative; what matters is whether it models p(x) (or p(x|y)).

**Q2 → C, D**

A generative model is a distribution p_model(x) that we draw samples from. Drawing is random, so two draws give two different x. A deterministic function g() has a single output: it is a point mass, which cannot cover a whole distribution of plausible images. The novelty requirement rules out memorization, since a model that returns training images exactly has p_model concentrated on the training set.

- A: ✗ Generative modeling is usually unsupervised; labels are optional and only needed for conditional generation.
- B: ✗ This is the textbook example of what is not generative. Averaging pixels is deterministic and yields one output.
- C: ✓ Correct. The “generative mandate”: deterministic calculations always return the same output.
- D: ✓ Correct. The goal is new observations that mimic the training-data patterns, not copies of them.

**Q3 → D**

A parametric model is a family of densities p_θ(x) described by a finite number of parameters. For the box family the density is 0 outside the box and constant inside it, with the constant chosen so that the density integrates to 1 over the sample space.

- A: ✗ A center alone does not fix the box’s width and height.
- B: ✗ That describes squares only. The orange box can be any rectangle.
- C: ✗ The density is defined everywhere, but it is parameterized by a finite set of numbers. That finiteness is the definition of a parametric model.
- D: ✓ Correct. Four numbers uniquely define each box, and therefore each density in the family.

**Q4 → C**

For independent observations L(θ|X) = ∏ p_θ(x_i). Under a uniform box, any point outside has density 0, so one such point makes the whole product 0 (log-likelihood −∞). The code below evaluates three boxes on the same data.

- A: ✗ The likelihood of i.i.d. data is a product, not an average.
- B: ✗ Likelihood is not the fraction of area covered. It depends on the density at the observed points.
- C: ✓ Correct. One zero factor in ∏ p_θ(x_i) makes the whole product zero.
- D: ✗ log(0) = −∞ is a perfectly meaningful log-likelihood. The likelihood itself is simply 0.

**Q5 → B**

MLE finds θ̂ = argmax_θ ℓ(θ|X). Equivalently, generative modeling minimizes the negative log-likelihood, where θ are the network weights. The log is used because multiplying thousands of small terms is numerically unstable.

- A: ✗ Neural-network log-likelihoods are generally non-convex. The log does not make them convex.
- B: ✓ Correct. The code below shows 1,000 probabilities multiplying to exactly 0.0 while the log-sum is a normal number. Sums are also easier to differentiate.
- C: ✗ Densities can exceed 1. That is not the reason for using logs.
- D: ✗ Log is strictly monotonic, so the argmax is unchanged.

**Q6 → A, B, C**

The three approaches are: (1) constrained explicit, where the density is modeled but constrained to be tractable; (2) approximate explicit, where a tractable approximation of the density is modeled; and (3) implicit, where a stochastic generating process is modeled without a density.

- A: ✓ Correct. GANs are the canonical implicit model.
- B: ✓ Correct. VAEs optimize a variational bound, EBMs use Markov-chain sampling, and diffusion models learn to denoise via a bound.
- C: ✓ Correct. Ordering constraints (AR) and invertible functions (flows) keep the density calculable.
- D: ✗ VAEs explicitly model an approximation (the ELBO) of the density, so they are approximate explicit models.
- E: ✗ The forward kernel is closed-form, but p(x) itself is only bounded through the ELBO. Diffusion models are classed as approximate.

**Q7 → D**

The conditional generative model estimates p(x|y). Sampling from p(x|y=apple) restricts generation to the slice of data space with that label. Classifier-free guidance in diffusion models is the same idea in practice.

- A: ✗ The class prior tells you how common apples are. It cannot generate an apple.
- B: ✗ That is the discriminative objective.
- C: ✗ Conditioning is a standard way to guide generation (e.g., classifier-free guidance in diffusion).
- D: ✓ Correct. Conditioning on y = apple steers sampling toward apple images.

**Q8 → B**

Rather than modeling pixels directly, we model a compact latent space where each point summarizes an observation. Sampling a new latent point and decoding it produces new data, including tins not in the training set. Editing the latent point (e.g., increasing height) makes targeted, intuitive changes.

- A: ✗ The point is to learn the latent factors and the decoder from data. Hand-coding does not scale to factors you cannot name, such as lighting, pose or style.
- B: ✓ Correct. Height and width form a 2-D latent space for tins, and a learned decoder maps (h, w) back to pixels.
- C: ✗ Kernel-style lifting is a different idea. Representation learning here compresses.
- D: ✗ That is memorization, which cannot produce novel tins.

**Q9 → B, D, E**

A 64×64 RGB image lives in a 12,288-dimensional space with 256^12288 possible pixel settings, almost all of which look like noise. Even millions of images cover a vanishingly small fraction of that space. Computing p(x) means integrating over latent variables or normalizing over the whole space, which has no closed form for a neural network. Each model family works around this in a different way: an ordering (autoregressive), a bound (VAE, diffusion), or no density at all (GAN).

- A: ✗ Images are usually treated as continuous. Densities are well defined.
- B: ✓ Correct. Each model family tackles this intractability differently.
- C: ✗ There is strong demand: content generation, rendering and advertising now run on generative models offered as cloud services.
- D: ✓ Correct.
- E: ✓ Correct.

**Q10 → D**

Accuracy: if p_model is high for a generated observation it should look like it came from p_data, and if low it should not. Generation: it should be easy to sample a new observation. Representation: it should be possible to understand how high-level features are represented by p_model.

- A: ✗ Determinism contradicts the generative mandate.
- B: ✗ These are engineering concerns. They say nothing about whether p_model matches p_data.
- C: ✗ None of these say whether samples look real, are easy to draw, or have interpretable factors.
- D: ✓ Correct. High p_model should mean the sample looks real; sampling should be easy; features should be interpretable.

**Q11 → A**

Lecture details: start small (e.g., 7B models) in a playground such as SageMaker JumpStart; adapt by fine-tuning and aligning to helpful, honest and harmless values; establish metrics; optimize for inference before deployment on endpoints; then monitor with tools like CloudWatch and CloudTrail.

- A: ✓ Correct. Six stages, starting from a single well-defined use case.
- B: ✗ Use-case identification comes first, and evaluation precedes deployment.
- C: ✗ The lifecycle explicitly starts from existing foundation models instead of training from scratch.
- D: ✗ Missing stages, and fine-tuning happens before deployment.

**Q12 → B, C, D**

Shared core principles: Traceability, Reliability, Lawfulness, Accountability, Governability, Equity. Military-specific concerns included adversarial AI, human–machine teaming and the arms race. Healthcare concerns included empathy, autonomy and privacy.

- A: ✗ Profit is a business goal, not an ethical principle.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✗ Autonomy appears as a healthcare concern, not as an unconstrained principle. Governability implies human oversight.

**Q13 → A**

Given x(s), the source ODE runs forward to the latent x(l); the target, reverse ODE then constructs x(t). Because each diffusion model is trained independently, the method can use pre-trained conditional diffusion models.

- A: ✓ Correct. Two diffusion models share the latent space reached by their deterministic ODEs.
- B: ✗ That describes CycleGAN-style training, not DDIBs.
- C: ✗ No VAE is involved.
- D: ✗ DDIBs do not need paired data or adversarial training.

**Q14 → B**

The difference is the training signal. Supervised learning sees the correct answer y for each x. Unsupervised learning sees only x. RL sees a scalar reward that may arrive many steps after the action that earned it, so the agent must learn a policy over sequences of actions (the credit-assignment problem).

- A: ✗ Dimensionality reduction is an unsupervised technique, not the defining feature of RL.
- B: ✓ Correct. The cycle is observe → act → improve from reward → environment transitions.
- C: ✗ That is supervised learning.
- D: ✗ That is unsupervised learning.

**Q15 → D**

Parametric modeling structures the search for p_model: choose a family (e.g., uniform boxes, Gaussians, neural networks), then estimate θ by maximum likelihood.

- A: ✗ Parametric families are families of probability densities.
- B: ✗ Likelihood is exactly the tool used to compare members of the family.
- C: ✗ Parametric families rarely contain p_data exactly. We look for the best member.
- D: ✓ Correct. MLE then picks the θ that makes the observed data most likely.

**Q16 → A**

Class 1 approximate density models: VAEs (latent variable plus a variational approximation of the joint density), energy-based models (approximate methods via Markov-chain sampling) and diffusion models (approximate the density by learning to gradually denoise a corrupted image).

- A: ✓ Correct.
- B: ✗ Autoregressive models are tractable explicit models with an exact likelihood.
- C: ✗ Flows are tractable explicit models built from invertible functions, and they give exact densities.
- D: ✗ GANs are implicit models. They define no density at all.

**Q17 → A**

Because every step is invertible with a computable Jacobian, the change-of-variables formula gives the exact density of complex distributions built from a simple one.

- A: ✓ Correct.
- B: ✗ That describes GANs.
- C: ✗ That describes VAEs and diffusion models.
- D: ✗ That describes autoregressive models.

**Q18 → A, B, C**

Sample space ≠ support of p_data. The model’s density (the orange box) must integrate to 1 over the whole sample space, being 0 outside the box and constant inside.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✗ The sample space contains every value x can take. Sea points are in it but have (near) zero true density.

**Q19 → C**

A density describes relative likelihood for a continuous variable; only integrals over regions are probabilities. For example, a N(0, 0.1²) density peaks at about 3.99, yet it is valid because its integral is 1.

- A: ✗ The uniform box density is discontinuous at its edges yet valid.
- B: ✗ Densities can exceed 1. A narrow Gaussian peaks well above 1.
- C: ✓ Correct.
- D: ✗ Many valid densities are skewed.

**Q20 → B, C, D**

Clustering is used for market segmentation and image compression. Dimensionality reduction helps visualization, noise reduction and computational efficiency. Generative models are usually unsupervised because they model p(x), which needs no labels.

- A: ✗ That is supervised, discriminative learning.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct. It sits in the taxonomy under unsupervised learning.

**Q21 → A**

The shift came as cloud services began offering generative modeling via APIs: automated content generation, visual product rendering and brand-tailored advertising.

- A: ✓ Correct.
- B: ✗ Not a reason given.
- C: ✗ Both need data. Generative models are usually unsupervised.
- D: ✗ They run on GPUs.

**Q22 → D**

The likelihood is ∏ p(xᵢ). The uniform density is 0 outside the box, so a single outside point makes the product 0 and its log −∞. Among boxes that contain every point, the score n·log(1/area) is highest for the smallest box, so the MLE is the tight bounding box.

- A: ✗ A uniform density gives no partial credit for distance.
- B: ✗ The area is well defined. The function returns early anyway.
- C: ✗ Nothing is clipped. The early return gives −inf.
- D: ✓ Correct. That box cannot have generated the data.

**Q23 → D**

Each factor is at most 0.5, so the product of 1,000 of them is below 0.5^1000 ≈ 1e−301, at the edge of float64’s range (about 1e−308), and with smaller factors it falls to exactly 0. Sums of logs stay in an ordinary numeric range.

- A: ✗ Underflow gives 0.0 silently, without an error.
- B: ✗ The product underflows.
- C: ✗ log is monotonic, so the argmax is unchanged.
- D: ✓ Correct. This is why we maximize the log-likelihood.


---

## Class 2 · Deep Learning (Vision ↔ NLP)

**Q24.** ○ *Single answer.* A Conv2D layer has 5 filters of size 4×4 applied to a 3-channel input. Ignoring biases, how many learnable weights does it have?

- ○ **A.** (4 × 4 × 3 + 1) × 5 = 245, which is the count without biases
- ○ **B.** 4 × 4 × 3 × 5 = 240
- ○ **C.** 32 × 32 × 3 × 5, because weights scale with the image size
- ○ **D.** 4 × 4 × 5 = 80

**Q25.** ○ *Single answer.* Compute the total learnable parameters for: Conv(4×4, 3→10) → Conv(3×3, 10→20) → Flatten (1,280 units) → Dense(10).

- ○ **A.** 15,120
- ○ **B.** 16,400, because Flatten adds one weight for each of its 1,280 output units and then one bias
- ○ **C.** 12,810
- ○ **D.** 14,630

**Q26.** ☐ *Select all that apply.* Which statements about the AlexNet design are correct? Select all that apply.

- ☐ **A.** With ReLU, biases start slightly positive so every layer begins with nonzero output and gradient
- ☐ **B.** Convolutional layers change the depth (number of channels) of the data
- ☐ **C.** Every convolutional layer uses sigmoid activations because ReLU had not yet been introduced in 2012
- ☐ **D.** Max-pooling layers downsample height and width; AlexNet uses 3×3 max-pooling with stride 2
- ☐ **E.** The classification head is a single linear layer with no bias

**Q27.** ○ *Single answer.* A residual (skip) connection computes f(x) = C(x) + x. What does the convolutional path C learn, and why does this help very deep networks?

- ○ **A.** C learns the residual f(x) − x; identity is just C = 0, and gradients flow through the skip
- ○ **B.** C learns the full mapping f(x); the skip only adds regularization noise
- ○ **C.** C learns to output zero always, so the network reduces to a shallow linear model
- ○ **D.** C learns x − f(x), and the skip connection performs channel-wise concatenation of the input and output rather than an addition

**Q28.** ○ *Single answer.* Which architecture is built from repeated inverted residual bottlenecks with depthwise convolutions?

- ○ **A.** DenseNet
- ○ **B.** ResNet-50
- ○ **C.** MobileNetV2
- ○ **D.** AlexNet, in its original two-GPU form with grouped convolutions

**Q29.** ☐ *Select all that apply.* Which statements correctly distinguish transfer learning from fine-tuning, as presented? Select all that apply.

- ☐ **A.** Fine-tuning is considered a specialized type of transfer learning
- ☐ **B.** Transfer learning requires more labeled data than fine-tuning because it trains all layers from scratch
- ☐ **C.** Transfer learning typically freezes the pretrained layers and trains only a new head
- ☐ **D.** Fine-tuning updates weights across the model and needs more data and compute

**Q30.** ○ *Single answer.* When fine-tuning, the learning rate is set too high. What failure mode results?

- ○ **A.** Catastrophic forgetting, which destroys the valuable pretrained knowledge
- ○ **B.** Exposure bias, where the model has never seen its own predictions as inputs during training
- ○ **C.** Mode collapse, where the network maps many different inputs to the same few outputs
- ○ **D.** Posterior collapse, where the pretrained layers stop sending any signal to the new classification head

**Q31.** ○ *Single answer.* On CIFAR-10, the vanilla dense network reached 50.89% test accuracy and the CNN about 70%. What is the main reason for the gap?

- ○ **A.** CNNs have far more learnable parameters than dense networks, so they can memorize more of the 50,000 training images
- ○ **B.** CIFAR-10 has only 10 classes, which favors convolution
- ○ **C.** Dense networks cannot use ReLU activations, so they are stuck with saturating sigmoids that slow learning
- ○ **D.** Local, weight-shared filters exploit spatial structure; a flattened dense net ignores pixel adjacency

**Q32.** ☐ *Select all that apply.* Generative Latent Optimization (GLO) was used to disentangle the sources of GAN success. Which statements are correct? Select all that apply.

- ☐ **A.** GLO keeps (A1) by using a deep convolutional generator but drops (A2), with no discriminator
- ☐ **B.** GLO shows that the adversarial game, not the convolutional architecture, is the dominant factor behind GAN image quality
- ☐ **C.** GLO outperformed GANs on every dataset it was tested on, including the complex LSUN scenes, while also training faster
- ☐ **D.** GAN success is split into (A1) the convnet inductive bias and (A2) the adversarial protocol
- ☐ **E.** GLO jointly optimizes the generator and each image’s latent vector to minimize reconstruction error

**Q33.** ○ *Single answer.* GAN training is described as seeking a saddle point. What does this mean?

- ○ **A.** A minimum for one player and a maximum for the other: a minimax equilibrium
- ○ **B.** A point where every gradient is zero and the Hessian is positive definite in all directions, i.e., a strict local minimum
- ○ **C.** The point in training at which the learning rate is halved, which stabilizes the two players
- ○ **D.** A point that is a global minimum of a single shared loss function

**Q34.** ○ *Single answer.* Why are GPUs preferred to CPUs for deep learning?

- ○ **A.** GPUs run at higher clock speeds than any CPU, so each individual operation finishes sooner
- ○ **B.** They maximize throughput on parallel arithmetic such as matrix multiplies
- ○ **C.** GPUs are optimized for low-latency serial execution of complex branching code
- ○ **D.** GPUs have no caches, which removes memory latency

**Q35.** ○ *Single answer.* The F1 score is defined as

- ○ **A.** the arithmetic mean of precision and recall, (P + R) / 2
- ○ **B.** the harmonic mean of precision and recall, 2PR / (P + R)
- ○ **C.** recall divided by precision, so that it equals 1 when the two are balanced
- ○ **D.** the fraction of all predictions that are correct across every class, regardless of class imbalance

**Q36.** ○ *Single answer.* How has the flow of ideas between NLP and computer vision changed over time?

- ○ **A.** Vision abandoned transfer learning, while NLP adopted it from computer vision only after the arrival of large language models
- ○ **B.** NLP has always led vision, since CNNs were invented for text
- ○ **C.** Vision and NLP have always developed independently
- ○ **D.** NLP once borrowed from vision; today vision borrows from NLP (attention, ViT)

**Q37.** ☐ *Select all that apply.* Which statements about pooling layers are correct? Select all that apply.

- ☐ **A.** Max pooling increases the number of channels, which is how a CNN grows deeper feature maps over its layers
- ☐ **B.** 2×2 max pooling keeps only the maximum value in each group
- ☐ **C.** Pooling layers have no learnable parameters
- ☐ **D.** Average pooling averages the values in each group

**Q38.** ○ *Single answer.* A Conv2D layer uses kernel size 3×3, 64 input channels and 128 filters, with bias. How many learnable parameters does it have?

- ○ **A.** 73,856
- ○ **B.** 73,728
- ○ **C.** 8,320
- ○ **D.** 1,152, because each filter is 3×3 and is shared across all 128 output channels

**Q39.** ○ *Single answer.* In tf.keras.layers.Conv2D, what does padding='same' do with stride 1?

- ○ **A.** Adds no padding, so the output shrinks
- ○ **B.** Forces all filters to share the same weights
- ○ **C.** Zero-pads the input so the output keeps the same height and width
- ○ **D.** Copies the edge pixels outward so that the convolution can see a mirror image of the border

**Q40.** ☐ *Select all that apply.* Why are pretrained vision models needed? Select all that apply.

- ☐ **A.** Architectures like ResNet, Xception and MobileNet have millions of parameters
- ☐ **B.** They encode visual features learned from huge datasets like ImageNet
- ☐ **C.** Pretrained models are guaranteed to specialize perfectly to any target domain without further adaptation
- ☐ **D.** Training such large models from scratch on a small dataset is not feasible

**Q41.** ○ *Single answer.* In the transfer-learning workflow, which step comes right after removing the pretrained model’s prediction head?

- ○ **A.** Add a small custom classification head for the new classes
- ○ **B.** Deploy the model
- ○ **C.** Retrain the entire network from random initialization so that ImageNet-specific features are removed
- ○ **D.** Freeze all weights including the new head

**Q42.** ○ *Single answer.* In a deep CNN’s feature hierarchy (input → low-level → mid-level → high-level units), what does a mid-level unit typically represent?

- ○ **A.** The abstract concept “smiling”, which summarizes the whole face into a single high-level label
- ○ **B.** Mid-level parts such as eyes or teeth
- ○ **C.** Simple edges and textures
- ○ **D.** Raw pixel values for a single color channel

**Q43.** ○ *Single answer.* DenseNet uses 1×1 convolutions in its transition blocks. What do they do?

- ○ **A.** Double the spatial resolution
- ○ **B.** Halve the number of channels
- ○ **C.** Replace the batch normalization layers, which are not used anywhere else in the DenseNet blocks
- ○ **D.** Add skip connections by element-wise addition

**Q44.** ○ *Single answer.* What does model.summary() report for this layer?

```python
inputs = layers.Input(shape=(32, 32, 3))
x = layers.Conv2D(filters=32, kernel_size=(3, 3))(inputs)
```

- ○ **A.** Output (None, 32, 32, 32), 864 parameters
- ○ **B.** Output (None, 30, 30, 3), 896 parameters, because Conv2D keeps the number of input channels
- ○ **C.** Output (None, 32, 32, 3), 28 parameters
- ○ **D.** Output (None, 30, 30, 32), 896 parameters

**Q45.** ○ *Single answer.* After MaxPooling2D(2) the tensor is (None, 15, 15, 32). What is the shape and parameter count after this layer?

```python
x = layers.MaxPooling2D(2)(x)          # (None, 15, 15, 32)
x = layers.Conv2D(64, 3, strides=2, padding="same", activation="relu")(x)
```

- ○ **A.** (None, 15, 15, 64), 18,496, since padding='same' always keeps the spatial size whatever the stride
- ○ **B.** (None, 8, 8, 64), 18,496
- ○ **C.** (None, 7, 7, 64), 18,432
- ○ **D.** (None, 8, 8, 32), 9,248

**Q46.** ○ *Single answer.* Which weights change when model.fit runs?

```python
base = tf.keras.applications.ResNet50(include_top=False, weights="imagenet", pooling="avg")
base.trainable = False
model = tf.keras.Sequential([base, layers.Dense(10, activation="softmax")])
model.compile(optimizer=tf.keras.optimizers.Adam(1e-3), loss="sparse_categorical_crossentropy")
model.fit(x_train, y_train, epochs=5)
```

- ○ **A.** Only the batch-normalization layers inside ResNet50, because they always stay trainable when the base is frozen
- ○ **B.** None, because frozen models cannot be compiled
- ○ **C.** All ResNet50 weights and the Dense head
- ○ **D.** Only the new Dense(10) head; the ResNet50 weights are frozen

**Q47.** ○ *Single answer.* Continuing from the previous model, the student runs this. What is it, and why the tiny learning rate?

```python
base.trainable = True
for layer in base.layers[:-30]:
    layer.trainable = False
model.compile(optimizer=tf.keras.optimizers.Adam(1e-5), loss="sparse_categorical_crossentropy")
model.fit(x_train, y_train, epochs=5)
```

- ○ **A.** Pruning the last 30 layers
- ○ **B.** Training from scratch; the low LR prevents overfitting
- ○ **C.** Fine-tuning the top layers; the low LR avoids destroying the pretrained features
- ○ **D.** Transfer learning with every layer frozen, since layer.trainable = False is applied to the whole network

**Q48.** ○ *Single answer.* What does this residual block compute, and what must hold for the addition to work?

```python
def residual_block(x):                 # x: (None, H, W, 64)
    y = layers.Conv2D(64, 3, padding="same", activation="relu")(x)
    y = layers.Conv2D(64, 3, padding="same")(y)
    return layers.Activation("relu")(layers.Add()([x, y]))
```

- ○ **A.** It averages x and C(x)
- ○ **B.** It multiplies x by the conv output to act as a gate, like an LSTM, which is why the shapes must match
- ○ **C.** Concatenation of x and the conv output; channels may differ
- ○ **D.** f(x) = C(x) + x element-wise; C(x) must match x’s shape (64 channels here)


### Answer key — Class 2 · Deep Learning (Vision ↔ NLP)

**Q24 → B**

With biases the formula is (k_h × k_w × C_in + 1) × filters. The weight count, 240 here, does not depend on the input’s height or width, which is why convolutions are parameter-efficient.

- A: ✗ 245 is the count with one bias per filter; the question asks to ignore biases.
- B: ✓ Correct. Each filter is 4×4×3 and there are 5 independent filters.
- C: ✗ Convolution shares weights spatially; parameter count is independent of image size.
- D: ✗ This forgets that each filter spans all 3 input channels.

**Q25 → A**

Conv1: (4·4·3 + 1)·10 = 490. Conv2: (3·3·10 + 1)·20 = 1,820. Flatten: 0. Dense: 1,280·10 + 10 = 12,810. Non-parametric layers (Flatten, MaxPool) contain zero learnable parameters.

- A: ✓ Correct. 490 + 1,820 + 0 + 12,810 = 15,120.
- B: ✗ Flatten has zero learnable parameters.
- C: ✗ That is only the dense layer.
- D: ✗ This omits the 490 parameters of the first convolution.

**Q26 → A, B, D**

AlexNet: conv layers change depth, max-pool layers downsample spatially, ReLU everywhere, additive biases in all conv and FC layers, and a three-FC-layer classification head.

- A: ✓ Correct. This avoids dead units at initialization.
- B: ✓ Correct.
- C: ✗ AlexNet popularized ReLU; every conv layer is ReLU-activated.
- D: ✓ Correct. These are overlapping pooling windows.
- E: ✗ The head flattens the final feature map and feeds it through three fully connected layers, all with additive bias.

**Q27 → A**

He et al. (2016): deeper plain networks suffer degradation because solvers struggle to fit identity mappings with stacked nonlinear layers. The residual formulation H(x) = F(x) + x makes identity trivial. Li et al. (2017) show skips turn a chaotic 56-layer loss landscape into a smoother one.

- A: ✓ Correct. This addresses both the degradation problem and vanishing gradients.
- B: ✗ With the skip, C only needs to learn the residual.
- C: ✗ C = 0 is possible but not forced. It is learned only where identity is optimal.
- D: ✗ The sign is wrong, and ResNet skips use element-wise addition. Concatenation is DenseNet and U-Net style.

**Q28 → C**

MobileNetV2 repeats inverted residual bottlenecks: expand → depthwise conv → project, for mobile efficiency. ResNet and DenseNet use ReLU and batch normalization; DenseNet’s 1×1 transitions halve channel count.

- A: ✗ DenseNet concatenates features, uses 32-channel conv outputs and 1×1 transition layers that halve channels.
- B: ✗ ResNet uses standard (not inverted) bottleneck residual blocks.
- C: ✓ Correct. “dw-cnv” in the diagram denotes depthwise convolutions.
- D: ✗ AlexNet predates inverted residual bottlenecks.

**Q29 → A, C, D**

Workflow: load a pretrained model, remove the prediction head, add a small custom head, freeze the feature extractor, and train only the new layers. Fine-tuning goes further, adapting pretrained weights by backpropagation for higher task performance.

- A: ✓ Correct. Both reuse pretrained weights. Fine-tuning simply unfreezes more of them.
- B: ✗ Backwards: transfer learning needs the least data since most weights are frozen.
- C: ✓ Correct.
- D: ✓ Correct.

**Q30 → A**

Why it happens: the pretrained weights sit in a good basin. A large step on a small new dataset moves them far from it, and the generic features are overwritten by ones that fit only the new data. Remedies: (1) warm up the LR from a small value; (2) use per-layer LRs; (3) give early, generic layers a smaller LR than later, task-specific ones. The Keras example below uses a 100× smaller LR after unfreezing.

- A: ✓ Correct. A too-low LR causes the opposite problem: very slow convergence.
- B: ✗ An autoregressive sequence-model issue, unrelated to fine-tuning learning rates.
- C: ✗ A GAN failure mode.
- D: ✗ A VAE failure mode in which the decoder ignores the latent.

**Q31 → D**

CIFAR-10 has 60,000 32×32 RGB images in 10 mutually exclusive classes (6,000 per class). Random guessing gives 10%. CNN filters detect edges, then parts, then concepts. The code below runs a hand-written edge filter so you can see what a single filter computes.

- A: ✗ CNNs usually have far fewer parameters, because each filter is reused at every position (see the parameter count in the code).
- B: ✗ The class count does not favor any architecture.
- C: ✗ They can.
- D: ✓ Correct. The inductive biases of locality and translation equivariance fit images.

**Q32 → A, D, E**

GLO: pair each image with a random vector, train a generator to reconstruct the image from its vector, and optimize both. Competitive results without adversarial training suggest that much of a GAN’s success comes from the convnet prior.

- A: ✓ Correct.
- B: ✗ The finding points the other way: (A1), the convnet inductive bias, is a dominant factor.
- C: ✗ GLO performed worse than GANs on LSUN, though it reproduced GAN-like properties on CelebA, MNIST and SVHN.
- D: ✓ Correct.
- E: ✓ Correct. Each image is paired with a random vector that is then learned.

**Q33 → A**

GAN optimization is min_G max_D V(D, G). It is sensitive to initialization, architecture and hyper-parameters, because the two players chase a moving target and gradient descent can cycle instead of converging. When the discriminator becomes too accurate, generator gradients vanish (Arjovsky & Bottou, 2017).

- A: ✓ Correct. The generator and discriminator compete.
- B: ✗ That is a strict local minimum, not a saddle.
- C: ✗ Unrelated.
- D: ✗ GANs have two players with opposing objectives, not one shared minimum.

**Q34 → B**

CPU: few powerful cores, low latency, serial. GPU: thousands of ALUs, high throughput, parallel. Training is dominated by matrix multiplies, which are embarrassingly parallel.

- A: ✗ Clock speed is not the main advantage. Massive parallelism is.
- B: ✓ Correct.
- C: ✗ That describes CPUs.
- D: ✗ GPUs do have caches, which turn long-latency memory accesses into short ones.

**Q35 → B**

Precision is the accuracy of positive predictions for a class. Recall is the fraction of a class’s images correctly classified. F1 is their harmonic mean, so it is low if either is low.

- A: ✗ F1 uses the harmonic mean, which penalizes imbalance between the two.
- B: ✓ Correct.
- C: ✗ Not a standard metric.
- D: ✗ That is accuracy.

**Q36 → D**

Progression: vision moved from CNNs to foundation vision models to transfer learning; NLP moved from RNNs to Transformers to LLMs to transfer learning. Attention now appears in vision (ViT), and joint models like VisualBERT combine both.

- A: ✗ Both fields use transfer learning: CNN → foundation vision models, RNN → Transformers → LLMs.
- B: ✗ CNNs came from vision.
- C: ✗ The two fields have converged on the same architectures.
- D: ✓ Correct.

**Q37 → B, C, D**

The goal is to distill information by downsampling each channel. In AlexNet, 3×3 max pooling with stride 2 gives overlapping pooling.

- A: ✗ Pooling downsamples height and width. Channel count comes from the number of conv filters.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.

**Q38 → A**

Parameters per filter = k_h · k_w · C_in + 1 bias. Multiply by the number of filters. Height and width of the input do not matter.

- A: ✓ Correct. (3·3·64 + 1) · 128.
- B: ✗ This forgets the 128 biases.
- C: ✗ That would be a 1×1 convolution: (64 + 1) · 128.
- D: ✗ Each output channel has its own filter, spanning all 64 input channels.

**Q39 → C**

With stride 2 and padding='same', the output size is ceil(input/2), which is why the autoencoder encoder halves 32 → 16 → 8 → 4.

- A: ✗ That is padding='valid'.
- B: ✗ Unrelated to padding.
- C: ✓ Correct.
- D: ✗ Keras uses zero padding, not reflection.

**Q40 → A, B, D**

Benefits: rich visual knowledge, avoiding overfitting on small data, high performance from little data. Trade-off: limited domain specialization, which fine-tuning addresses. The COVID-19 chest X-ray paper is the real-world example given.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✗ Pretrained features come from a different domain, so specialization is limited. That is the reason to fine-tune.
- D: ✓ Correct, as it would overfit and be too costly.

**Q41 → A**

Steps: load model → remove head → add custom layers → freeze feature-extraction weights → train only the new layers.

- A: ✓ Correct.
- B: ✗ It has not been trained for the new task yet.
- C: ✗ That throws away the pretrained knowledge.
- D: ✗ The new head must stay trainable.

**Q42 → B**

A: input pixels → B: low-level edges → C: mid-level parts → D: high-level concepts. Features are learned from data, not hand-coded.

- A: ✗ That is unit D.
- B: ✓ Correct.
- C: ✗ That is unit B.
- D: ✗ That is unit A.

**Q43 → B**

DenseNet conv layers each produce 32 channels that are concatenated with earlier outputs, so channel count grows. Transition blocks compress it back.

- A: ✗ 1×1 convolutions do not change spatial size.
- B: ✓ Correct.
- C: ✗ DenseNet convolutions use batch normalization and ReLU.
- D: ✗ DenseNet connects by concatenation, not addition.

**Q44 → D**

Conv2D defaults: strides = 1, padding = 'valid'. Parameters = (k·k·C_in + 1)·filters, independent of image size.

- A: ✗ padding='valid' shrinks 32 to 30, and there are 32 biases.
- B: ✗ The output channel count equals the number of filters, 32.
- C: ✗ No.
- D: ✓ Correct. (3·3·3 + 1)·32 = 896; valid padding gives 32 − 3 + 1 = 30.

**Q45 → B**

Shape rules: ‘valid’ → ⌊(H − k)/s⌋ + 1; ‘same’ → ⌈H/s⌉. Pooling layers have no parameters.

- A: ✗ ‘same’ keeps the size only at stride 1. At stride 2 it is ⌈H/2⌉.
- B: ✓ Correct. (3·3·32 + 1)·64 = 18,496.
- C: ✗ ‘same’ with stride 2 gives ceil(15/2) = 8, and the bias count is missing.
- D: ✗ The output has 64 channels.

**Q46 → D**

include_top=False removes the 1,000-class ImageNet head; pooling='avg' gives a 2,048-d feature vector; the new head maps it to 10 classes. Training updates only 2,048·10 + 10 = 20,490 weights.

- A: ✗ Setting trainable = False on the base freezes its batch-norm layers too.
- B: ✗ The model compiles, and the trainable head updates.
- C: ✗ base.trainable = False freezes the ResNet.
- D: ✓ Correct. This is transfer learning (feature extraction).

**Q47 → C**

This is the typical two-stage recipe: (1) train the new head with the base frozen; (2) unfreeze the top block and recompile with a learning rate about 100× smaller. Recompiling is required for trainable-flag changes to take effect.

- A: ✗ Nothing is removed.
- B: ✗ The pretrained weights are still loaded.
- C: ✓ Correct. The early, generic layers stay frozen.
- D: ✗ Only base.layers[:-30] are frozen. The last 30 layers train.

**Q48 → D**

The conv path learns only the residual C(x) = f(x) − x. Gradients flow through the identity path unchanged, which is what lets 50 to 150 layer ResNets train.

- A: ✗ A plain sum, not an average.
- B: ✗ Add is a sum, not a product.
- C: ✗ layers.Add is element-wise addition, not concatenation.
- D: ✓ Correct. Otherwise a 1×1 conv projection is needed on the skip.


---

## SimCLR paper (Chen et al., 2020)

**Q49.** ☐ *Select all that apply.* Which are the four major components of the SimCLR framework? Select all that apply.

- ☐ **A.** A memory bank storing negative representations from previous batches so that many negatives are available
- ☐ **B.** A base encoder f(·), a ResNet, producing representation h
- ☐ **C.** A stochastic data augmentation module producing two correlated views (a positive pair)
- ☐ **D.** The NT-Xent contrastive loss
- ☐ **E.** A small MLP projection head g(·) mapping h to z, where the loss is applied

**Q50.** ○ *Single answer.* With a minibatch of N = 4096 images, how many negative examples does each positive pair have in SimCLR?

- ○ **A.** 8,192
- ○ **B.** 8,190, i.e., 2(N − 1)
- ○ **C.** None; negatives are sampled explicitly from a separate pool
- ○ **D.** 4,095

**Q51.** ○ *Single answer.* The NT-Xent loss for a positive pair (i, j) is ℓ_ij = −log [ exp(sim(z_i, z_j)/τ) / Σ_{k≠i} exp(sim(z_i, z_k)/τ) ]. What is sim(·,·), and what does the temperature τ do?

- ○ **A.** sim is the raw unnormalized dot product; τ is a margin that must be exceeded
- ○ **B.** sim is cosine similarity; τ scales the logits and sets how much hard negatives count
- ○ **C.** sim is the Euclidean distance; τ is the learning rate
- ○ **D.** sim is KL divergence between the two views’ projection-head outputs treated as probability distributions

**Q52.** ☐ *Select all that apply.* Which findings about data augmentation in SimCLR are correct? Select all that apply.

- ☐ **A.** Random cropping composed with color distortion stands out as the most effective pair
- ☐ **B.** AutoAugment, found via supervised search, clearly beat simple crop + strong color distortion for SimCLR
- ☐ **C.** No single transformation suffices to learn good representations
- ☐ **D.** Contrastive learning benefits from stronger color augmentation than supervised learning does
- ☐ **E.** Without color distortion, crops share color histograms, giving the network a shortcut

**Q53.** ○ *Single answer.* SimCLR compares three projection heads: identity, linear, and a nonlinear one-hidden-layer MLP. What did it find?

- ○ **A.** Linear and nonlinear heads perform identically, and z = g(h) is the better representation to keep for downstream tasks after pretraining
- ○ **B.** Nonlinear beats linear (~3%) and identity (>10%); h before the head beats z downstream
- ○ **C.** Performance depends strongly on the output dimension of z
- ○ **D.** No projection head is best, since any head discards information

**Q54.** ○ *Single answer.* Why does SimCLR use global batch normalization across devices during distributed training?

- ○ **A.** To reduce memory usage on each TPU core by storing the batch statistics only once, centrally
- ○ **B.** Because LARS cannot work with local batch statistics and diverges immediately at batch size 256 unless every device shares them
- ○ **C.** Positive pairs share a device, so per-device BN statistics leak a shortcut
- ○ **D.** To make the model invariant to color distortion

**Q55.** ☐ *Select all that apply.* Which statements about batch size, training length and optimization in SimCLR are correct? Select all that apply.

- ☐ **A.** Contrastive learning benefits less than supervised learning from longer training, so 100 epochs is close to optimal for it
- ☐ **B.** The LARS optimizer is used to stabilize large-batch training
- ☐ **C.** The default setup trains at batch size 256 for 1,000 epochs with plain SGD and no warmup
- ☐ **D.** Larger batches help most when training is short (e.g., 100 epochs); the gap shrinks with longer training
- ☐ **E.** Square-root learning-rate scaling can help, particularly for smaller batch sizes

**Q56.** ○ *Single answer.* Under the linear evaluation protocol on ImageNet, what did SimCLR with ResNet-50 (4×) achieve?

- ○ **A.** 76.5% top-1, matching a supervised ResNet-50
- ○ **B.** 85.8% top-1 with no labels at all
- ○ **C.** 69.3% top-1, which already matched a fully supervised ResNet-50 trained for 90 epochs
- ○ **D.** 92.6% top-1

**Q57.** ○ *Single answer.* What is the purpose of the linear evaluation protocol?

- ○ **A.** To fine-tune the entire network end-to-end with all labels
- ○ **B.** To compress the model into a linear network for deployment on mobile devices
- ○ **C.** To evaluate how many positive pairs the network correctly identifies among the 2N − 2 negatives in the contrastive task
- ○ **D.** To score representation quality with a linear classifier on the frozen encoder

**Q58.** ○ *Single answer.* Which statement about model size in SimCLR is correct?

- ○ **A.** Width helps but depth hurts contrastive learning, because deeper encoders tend to cause representation collapse
- ○ **B.** Both benefit, but the supervised–SimCLR gap shrinks as models grow
- ○ **C.** Model size has no measurable effect beyond ResNet-18
- ○ **D.** Bigger models help supervised learning but hurt contrastive learning

**Q59.** ○ *Single answer.* SimCLR is contrasted with generative approaches to representation learning. Which description fits SimCLR?

- ○ **A.** It requires image–text pairs, like CLIP
- ○ **B.** It generates or models pixels in input space, as autoencoders and GANs do
- ○ **C.** It relies on hand-designed pretext tasks such as rotation prediction or jigsaw puzzles
- ○ **D.** It is discriminative: it contrasts views of one image against other images

**Q60.** ○ *Single answer.* In SimCLR, how are two augmented views of the same image produced?

- ○ **A.** Two operators t and t′ are sampled independently from the augmentation family T
- ○ **B.** A GAN generates the second view
- ○ **C.** The same augmentation t is applied twice, giving identical views
- ○ **D.** One view is the original image and the other is augmented in the default training setup

**Q61.** ○ *Single answer.* With ℓ2 normalization removed from NT-Xent (raw dot products), what happened?

- ○ **A.** Training diverged immediately and no model could be trained at any temperature value
- ○ **B.** Contrastive accuracy and linear-evaluation accuracy both rose
- ○ **C.** Contrastive accuracy rose, but linear-evaluation accuracy got worse
- ○ **D.** Nothing changed

**Q62.** ☐ *Select all that apply.* Which loss functions did SimCLR compare against NT-Xent, and what was found? Select all that apply.

- ☐ **A.** Margin triplet loss
- ☐ **B.** NT-Xent required semi-hard negative mining to reach its best result, just as the other losses did
- ☐ **C.** Semi-hard negative mining helped the alternatives but still left them well below NT-Xent
- ☐ **D.** NT-Logistic loss

**Q63.** ○ *Single answer.* On transfer to other image classification datasets via fine-tuning, how did SimCLR compare with a strong supervised baseline?

- ○ **A.** It could not be fine-tuned
- ○ **B.** Better on all 12 datasets by more than ten points each, making supervised pretraining obsolete
- ○ **C.** It was worse on every dataset
- ○ **D.** On par or better on 10 of 12 datasets

**Q64.** ○ *Single answer.* Which encoder is used in the paper, and where is h taken from?

- ○ **A.** A ResNet; h is the output of the projection head’s final layer, the 128-d vector z
- ○ **B.** A ResNet; h is the output after the average-pooling layer
- ○ **C.** A ViT; h is the [class] token
- ○ **D.** An LSTM over image patches

**Q65.** ○ *Single answer.* SimCLR Table 3 trains an MLP to predict which transformation (rotation, noise, Sobel, color) was applied, using either h or g(h). What does it show?

- ○ **A.** g(h) keeps more transformation information than h
- ○ **B.** Both are equally informative, since g is just an invertible linear map of h of the same dimension
- ○ **C.** Neither can predict color-vs-grayscale
- ○ **D.** h keeps far more (e.g., rotation 67.6% vs 25.6%): g discards what the contrastive loss ignores

**Q66.** ○ *Single answer.* In the asymmetric augmentation ablation (Figure 5), what does the average linear accuracy look like for a single transformation versus crop + color?

- ○ **A.** Single transformations stay low even when positives are easy; crop + color reaches 56.3
- ○ **B.** Augmentation order does not matter
- ○ **C.** Rotation + Sobel is the best pair, beating crop and color by a wide margin on every setting
- ○ **D.** Single transformations already reach about 64%

**Q67.** ○ *Single answer.* Why do the authors use linear warmup plus cosine decay with LARS at batch size 4096?

- ○ **A.** Cosine decay is needed because NT-Xent is not differentiable
- ○ **B.** LARS removes the need for a temperature
- ○ **C.** Warmup is used only to save memory on the TPU cores during the first few epochs of training
- ○ **D.** Large-batch SGD is unstable; LARS plus warmup stabilizes it

**Q68.** ○ *Single answer.* With N = 4 images (8 embeddings), how many candidates compete in the softmax for each row, and how many of them are negatives?

```python
z = l2_normalize(np.concatenate([z_view1, z_view2]))   # (2N, d), N = 4
sim = z @ z.T / tau
np.fill_diagonal(sim, -np.inf)
labels = np.r_[np.arange(N, 2*N), np.arange(N)]
loss = cross_entropy(sim, labels)
```

- ○ **A.** 7 candidates: 1 positive and 6 negatives, i.e., 2(N − 1)
- ○ **B.** 8 candidates, 7 negatives
- ○ **C.** 1 candidate
- ○ **D.** 4 candidates, 3 negatives, since only the first augmented view of each image is used

**Q69.** ○ *Single answer.* After pretraining, the student calls the following. Which object should be used to produce features for the downstream classifier?

```python
encoder = create_encoder()                  # f(.)
projection_head = create_projection_head()  # g(.)
# ... contrastive training on projection_head(encoder(x)) ...
features = ???(x_test)
```

- ○ **A.** projection_head alone, applied directly to the raw pixels without going through the encoder first
- ○ **B.** A new randomly initialized encoder
- ○ **C.** encoder(x), i.e., h before the projection head
- ○ **D.** projection_head(encoder(x))


### Answer key — SimCLR paper (Chen et al., 2020)

**Q49 → B, C, D, E**

SimCLR needs neither specialized architectures nor a memory bank. Two augmentations t, t′ ∼ T create x̃_i, x̃_j; f and g are trained to maximize agreement; after training g is discarded and h = f(x̃) is used downstream.

- A: ✗ SimCLR deliberately avoids memory banks and uses in-batch negatives with large batches.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✓ Correct.

**Q50 → B**

The paper’s example: batch size 8192 gives 16,382 negatives per positive pair. Large batches therefore supply many negatives, which is why SimCLR benefits from them.

- A: ✗ That is 2N, which incorrectly includes the anchor and its positive.
- B: ✓ Correct. There are 2N augmented views; excluding the anchor and its positive leaves 2N − 2.
- C: ✗ SimCLR does not sample negatives explicitly. The other in-batch views act as negatives.
- D: ✗ This counts only one view per image. Each image contributes two augmented views.

**Q51 → B**

NT-Xent stands for normalized temperature-scaled cross entropy. Looking at the gradients, ℓ2 normalization plus temperature weights negatives by their relative hardness, so it avoids the semi-hard negative mining that margin and logistic losses need. Linear evaluation: NT-Xent 63.9% versus at best 57.9% for the alternatives.

- A: ✗ Removing ℓ2 normalization raises contrastive accuracy but gives worse representations. A margin belongs to triplet losses.
- B: ✓ Correct. Table 5 shows τ ≈ 0.1 with ℓ2 normalization works best at batch 4096.
- C: ✗ sim is cosine similarity and τ is not a learning rate.
- D: ✗ No KL divergence is involved.

**Q52 → A, C, D, E**

Augmentations define the predictive task. Composing them makes the contrastive task harder but the representation better. Random crops subsume both global-to-local and adjacent-view prediction tasks.

- A: ✓ Correct.
- B: ✗ AutoAugment did not work better than crop + stronger color distortion.
- C: ✓ Correct. Composition is crucial.
- D: ✓ Correct. Table 1: SimCLR rises from 59.6 to 64.5 as strength increases, while supervised stays roughly flat.
- E: ✓ Correct. Figure 6 shows histograms alone can distinguish images.

**Q53 → B**

Hypothesis: the contrastive loss makes z invariant to augmentations, so g removes information (color, orientation) that may be useful downstream. Table 3 confirms h retains much more information about the applied transformation (e.g., rotation: 67.6% from h versus 25.6% from g(h)). Hence g is thrown away after pretraining.

- A: ✗ Nonlinear wins, and h beats z by more than 10%.
- B: ✓ Correct.
- C: ✗ With a head, results are similar regardless of the output dimension.
- D: ✗ No head was the worst, by more than 10%.

**Q54 → C**

Alternatives mentioned in the paper: shuffling examples across devices (MoCo) or replacing BN with layer norm (CPC v2).

- A: ✗ Global BN adds communication; it does not save memory.
- B: ✗ LARS addresses large-batch stability, not BN leakage.
- C: ✓ Correct. Aggregating BN mean and variance over all devices removes the shortcut.
- D: ✗ Unrelated to color invariance.

**Q55 → B, D, E**

Contrastive learning benefits more than its supervised counterpart from larger batches and longer training, which supply more negatives and more augmentation variety.

- A: ✗ It benefits more. Training up to 1,000 epochs keeps improving SimCLR, while supervised ResNets stop improving.
- B: ✓ Correct. Standard SGD/momentum with linear LR scaling can be unstable at large batch sizes.
- C: ✗ Default: batch 4096, 100 epochs, LARS with LR 4.8 = 0.3 × BatchSize/256, weight decay 10⁻⁶, 10-epoch warmup and cosine decay.
- D: ✓ Correct (Figure 9).
- E: ✓ Correct. Appendix B.1 covers square-root scaling.

**Q56 → A**

Linear evaluation trains a linear classifier on top of the frozen encoder and uses its test accuracy as a proxy for representation quality. ResNet-50 (1×) SimCLR: 69.3% top-1. ResNet-50 (4×): 76.5%. Semi-supervised with 1% labels: 75.5% top-5 (ResNet-50) and 85.8% (4×).

- A: ✓ Correct.
- B: ✗ 85.8% is top-5 accuracy when fine-tuning with 1% of labels.
- C: ✗ 69.3% is standard ResNet-50 SimCLR, and it does not match supervised.
- D: ✗ 92.6% is the top-5 accuracy with 10% labels for ResNet-50 (4×).

**Q57 → D**

Because the encoder is frozen and the classifier is linear, accuracy reflects how linearly separable, and therefore how useful, the learned features are.

- A: ✗ That is full fine-tuning, a separate experiment.
- B: ✗ Unrelated.
- C: ✗ Contrastive accuracy can be high while representations are poor (e.g., without ℓ2 normalization).
- D: ✓ Correct.

**Q58 → B**

A plausible reason: the contrastive task (pick 1 positive among 2N−2 negatives under heavy augmentation) is harder and less saturated than a 1,000-way label, so extra capacity keeps paying off.

- A: ✗ Depth also helps.
- B: ✓ Correct (Figure 7).
- C: ✗ Larger models give clear gains.
- D: ✗ Both benefit.

**Q59 → D**

The paper divides approaches into generative (pixel-level generation, which is expensive) and discriminative (pretext tasks or contrastive learning). Contrastive learning in the latent space achieved state-of-the-art results.

- A: ✗ SimCLR uses images only.
- B: ✗ Pixel-level generation is computationally expensive and not needed for representation learning.
- C: ✗ SimCLR avoids heuristic pretext tasks, which can limit generality.
- D: ✓ Correct.

**Q60 → A**

Default augmentations: random crop and resize (with flip), color distortion and Gaussian blur, applied sequentially.

- A: ✓ Correct.
- B: ✗ No generative model is involved.
- C: ✗ Identical views make the task trivial.
- D: ✗ That asymmetric setup was only used in the ablation, and it hurt performance.

**Q61 → C**

Table 5: with normalization and τ = 0.1, top-1 is 64.4%. Without normalization, contrastive accuracy is above 91% but top-1 is about 57%. Solving the pretext task better does not mean better features.

- A: ✗ Training ran, but the representations were worse.
- B: ✗ Only contrastive accuracy rose.
- C: ✓ Correct.
- D: ✗ Performance dropped significantly.

**Q62 → A, C, D**

The gradient analysis shows cross-entropy with ℓ2 normalization and temperature weights negatives by relative hardness; logistic and margin losses do not.

- A: ✓ Correct, one of the alternatives.
- B: ✗ NT-Xent weights negatives by hardness automatically and needs no mining.
- C: ✓ Correct. Their best was 57.9% versus 63.9%.
- D: ✓ Correct, one of the alternatives.

**Q63 → D**

Representations that are invariant to augmentation, rather than tuned to 1,000 ImageNet labels, carry over well to new label sets.

- A: ✗ Fine-tuning was evaluated.
- B: ✗ Too strong a claim.
- C: ✗ Not the result.
- D: ✓ Correct.

**Q64 → B**

The default projection head is a 2-layer MLP mapping the 2048-d h to a 128-d z. The framework places no constraints on the encoder architecture.

- A: ✗ That is z, which is not used downstream.
- B: ✓ Correct. For ResNet-50, h is 2048-dimensional.
- C: ✗ SimCLR uses ResNet.
- D: ✗ Not used.

**Q65 → D**

The contrastive objective rewards invariance to augmentations, so z = g(h) is pushed to forget them. Putting the loss on z lets h keep that detail, which a downstream task may need, such as orientation or color.

- A: ✗ This is reversed.
- B: ✗ g is a nonlinear MLP trained to be invariant. It is not invertible.
- C: ✗ Both can (h 99.3%, g(h) 97.4%). The gap is largest for rotation and Sobel.
- D: ✓ Correct. This is why h is used downstream.

**Q66 → A**

The lesson: a hard prediction task gives better representations. An easy task (one weak augmentation) is solved with shortcuts such as color histograms, which is the same failure you saw in your CL_Simple homework, where there was no second view at all.

- A: ✓ Correct. The highest single entries are crop (33.1) and cutout (25.6); color alone gets 18.8.
- B: ✗ The matrix is not symmetric. For example, crop then color is 56.3, while color then crop is 55.8.
- C: ✗ Crop + color is the standout pair.
- D: ✗ They do much worse.

**Q67 → D**

Training ResNet-50 at batch 4096 for 100 epochs on 128 TPU v3 cores takes about 1.5 hours. Global batch normalization is also required, to stop the per-device leakage shortcut.

- A: ✗ NT-Xent is smooth.
- B: ✗ τ is still needed.
- C: ✗ Warmup addresses stability, not memory.
- D: ✓ Correct. LR = 0.3 × BatchSize/256 = 4.8.

**Q68 → A**

Rows i and i + N are the two views of the same image. Masking the diagonal stops the trivial self-match, which was the bug in your CL_Simple notebook.

- A: ✓ Correct.
- B: ✗ The diagonal (self) is masked to −inf, so it is not a candidate.
- C: ✗ No.
- D: ✗ Both views of every image are in z.

**Q69 → C**

g(·) is only a training device: it gives the contrastive loss a space where invariance is enforced. Afterward it is thrown away. Linear evaluation then trains a linear layer on frozen h.

- A: ✗ The head expects encoder features, not pixels.
- B: ✗ That would discard what was learned.
- C: ✓ Correct. The paper finds h is more than 10% better than z under linear evaluation.
- D: ✗ z = g(h) has thrown away augmentation-related information. Use h.


---

## Reading assignments: ECMVAE (Mao et al., 2023) and MEMIT (Meng et al., 2023)

**Q70.** ○ *Single answer.* ECMVAE argues that the AVSBench baseline (TPAVI cross-attention) has a specific weakness. What is it?

- ○ **A.** Nothing forces audio to be used: it could regress masks from video alone
- ○ **B.** It uses a VAE whose latent space suffers from posterior collapse whenever several sound sources are present
- ○ **C.** It cannot process more than one video frame
- ○ **D.** It requires labeled audio categories

**Q71.** ☐ *Select all that apply.* How does ECMVAE factorize the latent space? Select all that apply.

- ☐ **A.** Modality-specific codes s_a (audio) and s_v (visual)
- ☐ **B.** A single 512-d latent shared by both modalities, with no specific codes, so the decoder cannot tell where information came from
- ☐ **C.** Fused codes sc_a = [c, s_a] and sc_v = [c, s_v], formed by concatenation, from which sampling is done
- ☐ **D.** A modality-shared code c, meant to capture the sound producer(s)

**Q72.** ○ *Single answer.* Why does ECMVAE factorize in a VAE latent space rather than directly in the deterministic feature space?

- ○ **A.** The decoder cannot read deterministic features
- ○ **B.** A VAE latent is continuous and regularized, which reliable factorization needs
- ○ **C.** VAE latents are smaller, so they train faster
- ○ **D.** Feature-space factorization would require labels for each modality, which AVSBench does not provide

**Q73.** ○ *Single answer.* ECMVAE’s difference loss is L_diff = ‖cᵀs_a‖²_F + ‖cᵀs_v‖²_F + ‖s_aᵀs_v‖²_F. When is it zero, and what does it enforce?

- ○ **A.** When the code subspaces are orthogonal; it keeps information from leaking between codes
- ○ **B.** When all codes are equal; it enforces agreement
- ○ **C.** Only when the codes are all zero vectors, so it is a weight-decay penalty
- ○ **D.** When the KL term is zero; it replaces the prior entirely, so no separate regularizer is needed

**Q74.** ○ *Single answer.* Which quantity does ECMVAE maximize to make the fused audio and visual codes share information, and how is it estimated?

- ○ **A.** I(SC_a; SC_v), via the Barber–Agakov lower bound E[log q(sc_a | sc_v)] + H(SC_a)
- ○ **B.** The reconstruction likelihood of the audio spectrogram
- ○ **C.** The KL divergence between sc_a and sc_v, estimated in closed form because both codes are Gaussian
- ○ **D.** The cosine similarity of the CLIP embeddings of each frame

**Q75.** ☐ *Select all that apply.* Why does ECMVAE use a Jensen–Shannon-based bound instead of a PoE or MoE KL? Select all that apply.

- ☐ **A.** The JS-based bound with a mixture prior trains more stably
- ☐ **B.** With a product of experts (PoE), one poorly modeled expert can ruin the joint distribution
- ☐ **C.** JS divergence is unbounded, so it penalizes mismatched modalities more strongly than KL does
- ☐ **D.** With MoE, the KL has no closed form and needs importance sampling

**Q76.** ○ *Single answer.* What problem does ECMVAE’s “hybrid” objective HELBO = α₁·ELBO + (1 − α₁)·L_GSNN address?

- ○ **A.** The lack of pretrained audio features
- ○ **B.** Class imbalance between sounding and silent pixels in the masks
- ○ **C.** Train/test mismatch: training samples the posterior (which sees y), testing the prior
- ○ **D.** The large memory cost of storing all five video frames in GPU memory at once during training

**Q77.** ☐ *Select all that apply.* Which statements match ECMVAE’s architecture and setup? Select all that apply.

- ☐ **A.** TPAVI fusion uses visual features as query and value, and audio as key
- ☐ **B.** The visual neck was enlarged from one convolution to ASPP with 512 channels to raise accuracy
- ☐ **C.** Visual backbone: PVTv2 or ResNet-50; audio: frozen VGGish (AudioSet), d = 128
- ☐ **D.** The decoder follows Panoptic-FPN and takes the TPAVI features plus the tiled latent codes

**Q78.** ○ *Single answer.* ECMVAE (PVT) reports S4 / MS3 mIoU of 81.74 / 57.84, against AVSBench’s 78.74 / 54.00. Which conclusion is best supported by the ablations?

- ○ **A.** Gains add up: adding audio, then factorization, then JS, and the losses each help
- ○ **B.** All of the gain comes from the larger backbone
- ○ **C.** Mutual-information maximization hurts S4 but helps MS3, so it should only be used for multiple sources
- ○ **D.** The orthogonality constraint alone explains the 3.84-point MS3 improvement over the AVSBench baseline

**Q79.** ○ *Single answer.* What limitation do the ECMVAE authors acknowledge, and what do they suggest?

- ○ **A.** It needs paired text captions
- ○ **B.** The model is too large to run in real time
- ○ **C.** Posterior collapse, where y is not encoded; they suggest contrastive or diffusion-based latents
- ○ **D.** It cannot be extended beyond two modalities, because the difference loss only works for exactly two codes

**Q80.** ○ *Single answer.* MEMIT models one MLP output matrix W as a linear associative memory. What is the closed-form update that inserts new key–value pairs (K₁, M₁)?

- ○ **A.** Δ = R K₁ᵀ (C₀ + K₁K₁ᵀ)⁻¹, with R = M₁ − W₀K₁ and C₀ = K₀K₀ᵀ
- ○ **B.** Δ = M₁K₁ᵀ
- ○ **C.** Δ = W₀⁻¹ M₁
- ○ **D.** Δ = −η ∇_W L, a single gradient step on the cross-entropy of the new facts

**Q81.** ○ *Single answer.* MEMIT never sees the pretraining keys K₀. How does it get C₀ = K₀K₀ᵀ?

- ○ **A.** By setting C₀ = I
- ○ **B.** As λ·E[kkᵀ], from layer inputs on ~100,000 Wikitext samples
- ○ **C.** It assumes C₀ = 0
- ○ **D.** By retraining the model on its original pretraining corpus and recording every key along the way

**Q82.** ○ *Single answer.* Why does MEMIT spread each edit over several layers (GPT-J: R = {3, …, 8}), unlike ROME’s single layer?

- ○ **A.** GPT-J’s attention layers cannot be edited, so the edit is copied into every MLP layer of the model
- ○ **B.** To make the edit reversible
- ○ **C.** Each layer stores a different relation type
- ○ **D.** Causal tracing implicates a range of MLPs, and spreading the edit keeps each weight change small

**Q83.** ○ *Single answer.* How does MEMIT compute the target vector zᵢ for an edit such as (Michael Jordan, plays sport, baseball)?

- ○ **A.** By averaging hidden states from many sentences that mention baseball, then subtracting the basketball average
- ○ **B.** zᵢ is the embedding of the token “baseball”
- ○ **C.** Gradient descent on δᵢ so that hᵢᴸ + δᵢ maximizes P(baseball), averaged over random text prefixes
- ○ **D.** By asking GPT-J to rephrase the fact

**Q84.** ☐ *Select all that apply.* How does MEMIT evaluate an edit? Select all that apply.

- ☐ **A.** Specificity (neighborhood): are related but different subjects, e.g., Kobe Bryant, unchanged?
- ☐ **B.** Fluency (generation entropy): does generated text avoid repetition such as “baseball baseball …”?
- ☐ **C.** Perplexity on the full pretraining corpus, recomputed after every single edit to detect forgetting
- ☐ **D.** Generalization (paraphrase): does the edit hold when the prompt is reworded?
- ☐ **E.** Efficacy: does the model prefer the new object on the exact edit prompt?

**Q85.** ○ *Single answer.* CounterFact, 10,000 edits on GPT-J: fine-tuning (FT-W) gets efficacy 99.4 but generation entropy 293.9 (vs about 622 unedited). What does this show?

- ○ **A.** Weight decay made FT-W too weak to change the model at all
- ○ **B.** FT-W is the best editor
- ○ **C.** High efficacy can hide damage: the fine-tuned model degenerates into repetitive text
- ○ **D.** Generation entropy is an unreliable metric that should be dropped from the evaluation altogether

**Q86.** ○ *Single answer.* How do ROME and MEND scale as the number of edits grows on CounterFact?

- ○ **A.** Both match MEMIT up to 10,000 edits, but they are slower, which is their only real disadvantage
- ○ **B.** Both improve with more edits
- ○ **C.** ROME drops from n ≈ 32 and MEND from n ≈ 6; MEMIT holds to 10,000
- ○ **D.** MEND is best at large n because its hypernetwork batches gradients

**Q87.** ○ *Single answer.* In MEMIT’s causal tracing on GPT-J, which observation justifies editing MLPs rather than attention at the last subject token?

- ○ **A.** Severing attention removes the causal effect, while severing MLPs has no effect
- ○ **B.** Attention layers in GPT-J have no learnable weights, so there is nothing in them that could be edited
- ○ **C.** Severing MLPs opens a large gap in the indirect effect, while severing attention barely changes it
- ○ **D.** MLPs are closer to the output layer

**Q88.** ☐ *Select all that apply.* Which limitations and caveats does the MEMIT paper state? Select all that apply.

- ☐ **A.** The same method could let a malicious actor insert false information into a model
- ☐ **B.** It handles only directional (subject, relation, object) facts, not symmetric or procedural knowledge
- ☐ **C.** It requires full access to the original pretraining data to estimate the key covariance C₀ accurately
- ☐ **D.** Some relations (e.g., athlete’s sport, P641) are harder to edit specifically
- ☐ **E.** “Tim Cook is CEO of Apple” and “The CEO of Apple is Tim Cook” must be edited separately


### Answer key — Reading assignments: ECMVAE (Mao et al., 2023) and MEMIT (Meng et al., 2023)

**Q70 → A**

ECMVAE treats audio as a “command” that selects which visible object is sounding. If the network can lower the loss using only salient visual objects, audio becomes optional. The paper’s ablation shows this matters: a CVAE without audio reaches 49.26 mIoU on MS3, versus 54.99 for the multimodal CMVAE.

- A: ✓ Correct. Implicit fusion gives no guarantee of each modality’s contribution.
- B: ✗ The baseline is not a VAE. Posterior collapse is a limitation ECMVAE lists for itself.
- C: ✗ The baseline processes all T = 5 frames.
- D: ✗ AVSBench supplies pixel masks, not audio labels used as targets.

**Q71 → A, C, D**

Three small encoders φ_c, φ_sa and φ_sv produce T × L codes (L = 16). The posterior networks take the ground-truth mask y as extra input; the prior networks do not. The ablation shows factorization (56.38 MS3 mIoU) beats a non-factorized model with 2× the latent size (55.09), so the gain comes from the structure, not the capacity.

- A: ✓ Correct, e.g., background noise or scene content.
- B: ✗ That is the non-factorized baseline. ECMVAE uses L = 16 per code.
- C: ✓ Correct. This is the efficient-sampling trick.
- D: ✓ Correct.

**Q72 → B**

This echoes Class 3: a plain AE gives a gappy, unstructured latent space, while the KL (or JS) term makes it smooth and centered. ECMVAE argues the continuity is a basic requirement for meaningful shared and specific subspaces.

- A: ✗ The decoder actually takes both the TPAVI features and the latent codes.
- B: ✓ Correct. AE factorization reached only 54.82 MS3 mIoU, against 56.38 for VAE factorization.
- C: ✗ Speed is not the argument.
- D: ✗ No per-modality labels are needed either way.

**Q73 → A**

This is the difference loss from Domain Separation Networks. In the ablation it adds +0.64 mIoU on MS3 (57.01 → 57.65), and t-SNE shows the three codes separating into distinct clusters. The Code & logic tab computes it for leaky and for orthogonal codes.

- A: ✓ Correct.
- B: ✗ Equal codes maximize the inner products, so this is the worst case.
- C: ✗ Zero codes satisfy it trivially, but non-zero orthogonal codes do too. It is not weight decay.
- D: ✗ It is an extra constraint added alongside the ELBO.

**Q74 → A**

I(A; V) ≥ E[log q(a | v)] + H(A), with a gap of E[KL(p(a|v) ‖ q(a|v))]. Because the VGGish audio encoder is frozen, H(SC_a) is treated as a constant, so L_sic = −E[log q(sc_a | sc_v)], averaged over posterior and prior samples (α₂ = 0.5). The Code & logic tab checks this bound on correlated Gaussians.

- A: ✓ Correct. q is a Gaussian with an MLP-predicted mean and variance.
- B: ✗ ECMVAE does not reconstruct audio. It predicts segmentation masks.
- C: ✗ Maximizing a divergence would push the codes apart, which is the opposite of the goal.
- D: ✗ CLIP is not used.

**Q75 → A, B, D**

Ablation (MS3 mIoU): KL 56.38 → PoE 57.35 → MoE 57.53 → JS 57.84. The JS term compares the posterior and the prior against their mixture f_K, which is MoE-like, keeping per-modality contributions without MoE’s sampling cost.

- A: ✓ Correct.
- B: ✓ Correct. Densities multiply, so a confident bad expert dominates.
- C: ✗ JS is bounded by log 2. That boundedness is part of why it is stable.
- D: ✓ Correct.

**Q76 → C**

In a conditional VAE, the posterior q(z | X, y) can peek at the ground truth during training, but at test time only the prior p(z | X) is available. Training on prior samples as well (the Gaussian stochastic neural network objective) closes this gap. The same idea is used for the MI term (α₂ = 0.5).

- A: ✗ VGGish already supplies pretrained audio features.
- B: ✗ That is handled by the weighted structure-aware loss, not the hybrid term.
- C: ✓ Correct. L_GSNN trains with prior samples too; α₁ = 0.5.
- D: ✗ Unrelated to memory.

**Q77 → A, C, D**

Training: Adam with lr 1e-4, batch size 4, 15 epochs on S4 and 30 on MS3. Loss weights λ = {0.001, 0.01, 0.5} for L_diff, L_sic and L_AVM, and β = 0.1 on the KL/JS terms. In S4 only the first frame is labeled (semi-supervised), so its mask is repeated five times to build the posterior.

- A: ✓ Correct.
- B: ✗ The reverse: ASPP became a single convolution, and 256 channels became 128. That makes ECMVAE smaller and faster (91.18M vs 101.32M parameters with PVT).
- C: ✓ Correct.
- D: ✓ Correct.

**Q78 → A**

Read ablation tables additively. CVAE (no audio) 49.26 → CMVAE (audio) 54.99 → factorized VAE 56.38 → JS divergence 57.84, with L_diff and L_sic helping within the last step. The multi-source setting gains most, because audio is needed to choose among several sounding objects.

- A: ✓ Correct. MS3 goes 49.26 → 54.99 → 56.38 → 57.84.
- B: ✗ Both methods use the same PVTv2 backbone.
- C: ✗ The full model (both losses) is best on both settings.
- D: ✗ It contributes about 0.6 points.

**Q79 → C**

Posterior collapse happens when the decoder ignores z, so the KL drives q(z | X, y) to equal the prior. The latent then carries no information about y. This links to Class 3 (the KL term) and Class 7 (diffusion models as richer latent models).

- A: ✗ No text is used.
- B: ✗ It is faster than AVSBench: 46 ms vs 53 ms with PVT.
- C: ✓ Correct.
- D: ✗ The authors say it can be extended to more modalities.

**Q80 → A**

Minimize Σ_old ‖W k − m‖² + Σ_new ‖W k − m‖². The normal equation (W₀ + Δ)(C₀ + K₁K₁ᵀ) = M₀K₀ᵀ + M₁K₁ᵀ, minus the pretraining optimum W₀C₀ = M₀K₀ᵀ, leaves Δ(C₀ + K₁K₁ᵀ) = R K₁ᵀ. The Code & logic tab runs this for 100 new facts.

- A: ✓ Correct. These are the normal equations for old plus new pairs.
- B: ✗ This ignores the old keys, so it would overwrite existing memories.
- C: ✗ W₀ is not square or invertible, and this form makes no sense.
- D: ✗ That is fine-tuning (FT-W), not MEMIT’s closed form.

**Q81 → B**

Old memories are modeled as a random sample of the inputs the layer sees, so their uncentered covariance is estimated from generic text. λ balances old against new: a larger λ protects existing associations more, but each new edit is fitted less exactly.

- A: ✗ The identity would ignore the real geometry of the keys.
- B: ✓ Correct. λ = 15,000 for GPT-J and 20,000 for GPT-NeoX.
- C: ✗ Then the update would ignore old memories and damage specificity.
- D: ✗ Avoiding retraining is the whole point.

**Q82 → D**

MLP outputs add into the residual stream, so the needed change δᵢ at layer L can be built from several smaller additions. Layers are updated in ascending order, re-collecting activations after each layer, because earlier edits change later inputs. Smaller per-layer norms improve robustness (Zhu et al., 2020).

- A: ✗ Only the critical range is edited, not every layer.
- B: ✗ Reversibility is not discussed.
- C: ✗ The paper does not assign relations to layers.
- D: ✓ Correct. Layer l writes (zᵢ − hᵢᴸ)/(L − l + 1) of the remaining gap.

**Q83 → C**

25 optimization steps with learning rate 0.5, with ‖δᵢ‖ clamped to at most ¾·‖hᵢᴸ‖ for GPT-J. Each zᵢ is computed independently, which is “embarrassingly parallel” (computed serially, 10,000 of them take 6.54 hours).

- A: ✗ That is closer to latent arithmetic, not MEMIT’s procedure.
- B: ✗ The target lives in hidden-state space at the last subject token, not in the embedding table.
- C: ✓ Correct. The prefixes help generalization.
- D: ✗ Paraphrases are used for evaluation, not for computing zᵢ.

**Q84 → A, B, D, E**

The overall Score is the harmonic mean of efficacy, paraphrase and specificity (ES, PS, NS). Consistency (RS) checks generated text against a reference Wikipedia text about the new object using TF-IDF similarity.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✗ Not one of the paper’s metrics.
- D: ✓ Correct.
- E: ✓ Correct.

**Q85 → C**

This is the trade-off MEMIT targets: forcing new facts in with gradient steps overwrites unrelated knowledge and fluency. MEMIT reaches ES 98.9, PS 88.6, NS 73.7 and GE 619.9, close to the unedited fluency.

- A: ✗ Efficacy of 99.4 shows it changed the model a lot.
- B: ✗ Its overall Score is 67.6, against 85.8 for MEMIT.
- C: ✓ Correct. Specificity is also low (46.9).
- D: ✗ It caught a real failure that the probability metrics missed.

**Q86 → C**

At small n, ROME generalizes slightly better than MEMIT, thanks to its hard equality constraint, at the cost of a little specificity. At 10,000 zsRE edits the Scores are MEMIT 50.7, FT-W 42.1, MEND 20.0 and ROME 2.6. Sequential single-fact edits accumulate damage.

- A: ✗ Both fail long before 10,000 edits.
- B: ✗ Both degrade.
- C: ✓ Correct. MEND at 10,000 barely changes the model.
- D: ✗ Its batched updates lose efficacy as n grows.

**Q87 → C**

Setup: corrupt the subject embeddings with Gaussian noise (3σ), restore one hidden state, and measure how much of the correct prediction returns. Repeat with that state’s MLP or attention frozen in the corrupted state. A large drop when the MLP is frozen means the MLP mediates recall. This is direct and indirect effects from Class 4, applied to real hidden states.

- A: ✗ This is reversed.
- B: ✗ Attention has W_Q, W_K, W_V and W_O.
- C: ✓ Correct. The MLP gap shrinks after layer 8, which sets R = {3…8}.
- D: ✗ The critical MLPs are early and middle layers.

**Q88 → A, B, D, E**

Edit requests must also be non-conflicting: no two edits may share (s, r) with different objects. Mixing relations has near-average effects, so performance is not hurt by edit diversity.

- A: ✓ Correct. This is in the ethics section.
- B: ✓ Correct.
- C: ✗ C₀ comes from about 100K Wikitext samples, not the pretraining data.
- D: ✓ Correct.
- E: ✓ Correct.


---

## Class 3 · Autoencoders & VAEs

**Q89.** ○ *Single answer.* A latent variable model describes Pr(x) indirectly. Which expression is the marginalization used for a continuous latent z?

- ○ **A.** Pr(x) = ∫ Pr(x | z) Pr(z) dz
- ○ **B.** Pr(x) = max_z Pr(x, z), taking only the single most likely latent configuration for each observed data point
- ○ **C.** Pr(x) = Pr(x | z) for z = 0
- ○ **D.** Pr(x) = Pr(z | x) Pr(x) / Pr(z)

**Q90.** ☐ *Select all that apply.* Consider the 1-D mixture of Gaussians viewed as a latent variable model. Which statements are correct? Select all that apply.

- ☐ **A.** The mixing weights λ_n may be negative as long as they sum to one
- ☐ **B.** Pr(x | z = n) is normal with mean μ_n and variance σ_n²
- ☐ **C.** Pr(x) is obtained by summing the weighted components: Σ_n λ_n · Norm(x; μ_n, σ_n²)
- ☐ **D.** Pr(x) must be unimodal, since each individual component is a single Gaussian with only one peak
- ☐ **E.** z is discrete, and the prior Pr(z) is categorical with probabilities λ_n

**Q91.** ○ *Single answer.* Why is training the nonlinear latent variable model by direct maximum likelihood intractable?

- ○ **A.** The decoder f[z, φ] is not differentiable with respect to its parameters, so gradients cannot be computed
- ○ **B.** The likelihood Pr(x|z) is not Gaussian, so no parametric form exists for evaluating it at all
- ○ **C.** The prior Pr(z) is unknown and must be learned jointly with φ, which makes the objective ill-posed in high dimensions
- ○ **D.** The integral ∫ Pr(x|z, φ) Pr(z) dz has no closed form and is hard to evaluate for a given x

**Q92.** ☐ *Select all that apply.* Which statements about the Evidence Lower Bound (ELBO) are correct? Select all that apply.

- ☐ **A.** Maximizing it with respect to θ can decrease the true log-likelihood while increasing the bound itself
- ☐ **B.** It depends on decoder parameters φ and variational parameters θ
- ☐ **C.** It lies everywhere below the log-likelihood log Pr(x|φ)
- ☐ **D.** It is tight when q(z|x, θ) equals the true posterior Pr(z|x, φ)
- ☐ **E.** It can be written as reconstruction term − KL(q(z|x,θ) ‖ Pr(z))

**Q93.** ☐ *Select all that apply.* Which statements about KL divergence are correct? Select all that apply.

- ☐ **A.** It is always ≥ 0, and equals 0 only when the two distributions are identical
- ☐ **B.** KL(p ‖ q) explodes to infinity if p assigns positive probability where q assigns zero
- ☐ **C.** It measures the information lost when q is used to approximate p
- ☐ **D.** It is symmetric, KL(p ‖ q) = KL(q ‖ p), so it is a true distance metric satisfying the triangle inequality

**Q94.** ○ *Single answer.* The VAE encoder outputs z_mean and z_log_var. What is the closed-form KL term to N(0, I) used in the implementation?

- ○ **A.** 0.5 · Σ (z_mean² + z_log_var²), the squared distance of the encoder outputs from the origin
- ○ **B.** −0.5 · Σ (1 + z_log_var − z_mean² − exp(z_log_var))
- ○ **C.** Σ (z_mean − z_log_var)²
- ○ **D.** −Σ log(z_mean)

**Q95.** ○ *Single answer.* Why does the VAE encoder output the log of the variance rather than the variance itself?

- ○ **A.** Log variance makes the KL term vanish, which leaves only the reconstruction loss to optimize
- ○ **B.** To make the latent dimensions correlated with one another, giving a full covariance matrix
- ○ **C.** Network outputs are unbounded but variance must be positive; exp(log_var) is always > 0
- ○ **D.** The log variance is required by the reparameterization trick, which only accepts values in (0, 1)

**Q96.** ○ *Single answer.* What does the reparameterization trick z = μ + σ ⊙ ε, with ε ~ N(0, I), accomplish?

- ○ **A.** It removes all randomness from the VAE, making it deterministic
- ○ **B.** It isolates randomness in ε so z is differentiable in μ and σ
- ○ **C.** It forces the encoder to output a full covariance matrix, capturing correlations between latent dimensions
- ○ **D.** It replaces the KL term in the loss

**Q97.** ☐ *Select all that apply.* The plain autoencoder trained on Fashion-MNIST with a 2-D latent space produced a problematic embedding. Which of the following are typical problems with such an embedding? Select all that apply.

- ☐ **A.** The distribution is not symmetric about (0, 0); many points have large positive y-values
- ☐ **B.** Points decoded from anywhere in the bounding box are guaranteed to look like realistic, well-formed clothing items
- ☐ **C.** Some clothing items occupy a very small area and others a much larger one
- ☐ **D.** There are large gaps between clusters containing few points

**Q98.** ○ *Single answer.* How does the VAE’s encoder differ from a plain autoencoder’s encoder?

- ○ **A.** The VAE encoder outputs class labels that the decoder then uses to choose which clothing type to draw
- ○ **B.** The VAE has no encoder; it samples latent vectors from the prior and then optimizes them directly with gradient descent
- ○ **C.** The AE maps each image to one point; the VAE maps it to a normal distribution around a point
- ○ **D.** The VAE encoder uses transposed convolutions

**Q99.** ☐ *Select all that apply.* Which effects does the KL loss term have on the latent space? Select all that apply.

- ☐ **A.** It forces each clothing class into its own separate region, since the KL term acts as a supervised class-separation loss
- ☐ **B.** It guarantees perfect pixel-level reconstructions
- ☐ **C.** It encourages the encoder to use the space around the origin symmetrically and efficiently
- ☐ **D.** It provides a well-defined distribution, N(0, I), from which to choose latent points for generation
- ☐ **E.** It reduces the chance of large gaps forming between point clusters

**Q100.** ○ *Single answer.* For the CelebA VAE, what changes were made compared to the Fashion-MNIST model?

- ○ **A.** Latent dimension 2, β = 0.001, and the decoder replaced by a GAN generator trained adversarially on the celebrity images
- ○ **B.** 3 input channels, latent dimension increased from 2 to 200, KL β factor of 2,000, batch norm after each conv
- ○ **C.** Latent dimension reduced to 1, grayscale input, β removed
- ○ **D.** Removal of the encoder

**Q101.** ○ *Single answer.* How is a “smile vector” built and used in VAE latent-space arithmetic?

- ○ **A.** Train a separate classifier for smiling and use its weights as the vector
- ○ **B.** Subtract the average non-smiling embedding from the average smiling one; add α times it to any z
- ○ **C.** Multiply the latent vector element-wise by a mask that zeros out every dimension except the one known to encode smiling
- ○ **D.** Randomly sample until a smiling face appears

**Q102.** ○ *Single answer.* Morphing between faces A and B uses z_new = z_A(1 − α) + z_B α. What happens as α goes from 0 to 1?

- ○ **A.** The model is retrained on every interpolated point to make sure each intermediate face decodes realistically
- ○ **B.** Decoded images transition gradually from face A to face B
- ○ **C.** The output jumps abruptly from A to B at α = 0.5
- ○ **D.** The image becomes pure noise at α = 0.5, since the midpoint lies outside the learned latent distribution

**Q103.** ○ *Single answer.* Ancestral sampling for Pr(x, y, z) = Pr(x) Pr(y|x) Pr(z|y) proceeds by

- ○ **A.** drawing x* ~ Pr(x), then y* ~ Pr(y|x*), then z* ~ Pr(z|y*)
- ○ **B.** sampling z first, then y, then x
- ○ **C.** Gibbs sampling all three variables jointly, cycling through each conditional until the chain converges to the joint
- ○ **D.** computing the marginal of each variable separately

**Q104.** ○ *Single answer.* A Conv2DTranspose layer with stride 2 is used in the decoder. What does it do?

- ○ **A.** Performs max pooling followed by a learned 1×1 convolution, keeping the spatial size unchanged
- ○ **B.** Upsamples: it produces a larger spatial output, typically with fewer channels
- ○ **C.** Halves the spatial size and doubles channels
- ○ **D.** Computes attention between feature-map positions so that every spatial location can aggregate information from every other

**Q105.** ○ *Single answer.* The Fashion-MNIST encoder takes a 32×32×1 input through three Conv2D layers (32, 64, 128 filters, 3×3, stride 2, padding same), then Flatten, then Dense(2). What is the shape before Flatten, and how many parameters does Dense(2) have?

- ○ **A.** 2×2×128 → 512 features; Dense(2) has 1,026 parameters, since each stride-2 layer halves the spatial size twice
- ○ **B.** 4×4×128 → 2,048 features; Dense(2) has 4,096 parameters
- ○ **C.** 4×4×128 → 2,048 features; Dense(2) has 2,048·2 + 2 = 4,098 parameters
- ○ **D.** 8×8×128 → 8,192 features; Dense(2) has 16,386 parameters

**Q106.** ○ *Single answer.* A Keras autoencoder reconstructs Fashion-MNIST pixels scaled to [0, 1] through a sigmoid output. Which loss fits, and why?

- ○ **A.** Mean absolute error between the 2-D latent vectors of each image and its augmented copy, as in contrastive learning
- ○ **B.** Hinge loss, because the decoder outputs signed margins rather than pixel intensities
- ○ **C.** Binary cross-entropy, appropriate for pixel values scaled to [0, 1] with a sigmoid output
- ○ **D.** Categorical cross-entropy over the 10 clothing classes

**Q107.** ☐ *Select all that apply.* ECMVAE (Explicit Conditional Multimodal VAE) for audio-visual segmentation. Which statements are correct? Select all that apply.

- ☐ **A.** It factorizes each modality’s latent into a shared code c and specific codes s_a, s_v
- ☐ **B.** It relies on implicit feature fusion so that the individual contribution of each modality stays hidden from the model
- ☐ **C.** It uses Jensen–Shannon divergence to balance sampling efficiency and generation quality
- ☐ **D.** A mutual-information maximization regularizer encourages maximally informative representations
- ☐ **E.** An orthogonality constraint keeps shared and specific codes exclusive and prevents information leakage

**Q108.** ○ *Single answer.* In ECMVAE’s view of multimodal information for audio-visual segmentation, what does the audio modality mainly contribute?

- ○ **A.** Scene context, in which the candidate sound producers usually occupy only a small portion of the frame
- ○ **B.** Category information about what kind of sound, and so what kind of source, is present
- ○ **C.** Nothing; the audio is used only as a regularizer
- ○ **D.** Precise pixel locations of sound producers

**Q109.** ○ *Single answer.* AVSBench evaluation settings S4 and MS3 refer to

- ○ **A.** Four-second and three-second clip lengths used for the single-frame and the multi-frame subsets
- ○ **B.** Spatial and Spectral metrics, measuring mask overlap and audio-frequency alignment respectively
- ○ **C.** Supervised and Multi-Shot training settings in which the number of labeled frames per video is varied
- ○ **D.** Single-Sound-Source segmentation and Multiple-Sound-Source segmentation

**Q110.** ○ *Single answer.* In the nonlinear latent variable model, which parts of the data are explained by f[z, φ] and which by σ²I?

- ○ **A.** f explains the noise, and σ²I explains the structure
- ○ **B.** f models the important structure; leftover detail is treated as spherical noise σ²I
- ○ **C.** σ²I is learned per pixel
- ○ **D.** Both model noise, because the latent z is pure noise and carries no information about the data

**Q111.** ○ *Single answer.* Bayes’ rule gives the posterior Pr(z | x, φ) = Pr(x|z, φ) Pr(z) / Pr(x|φ). Why is it not used directly in the VAE?

- ○ **A.** The posterior is always Gaussian, so it is unnecessary
- ○ **B.** The prior Pr(z) is unknown
- ○ **C.** The evidence Pr(x|φ) in the denominator is intractable
- ○ **D.** The likelihood is not differentiable with respect to z, which blocks every gradient-based method

**Q112.** ☐ *Select all that apply.* Which statements about the multivariate standard normal N(0, I) are correct? Select all that apply.

- ☐ **A.** The mean vector is all zeros
- ☐ **B.** The covariance matrix may be asymmetric, with cov(X, Y) ≠ cov(Y, X) when the variables are dependent
- ☐ **C.** Off-diagonal covariances are zero, so for a Gaussian the variables are independent
- ☐ **D.** The covariance is the identity matrix, so each variable has unit variance

**Q113.** ○ *Single answer.* Why does the plain autoencoder struggle to generate new images by sampling random latent points?

- ○ **A.** It has no decoder, so there is no network that maps a latent point back into the image space
- ○ **B.** Its encoder is stochastic
- ○ **C.** Its latent space is not forced to be continuous, so random points often decode poorly
- ○ **D.** Its decoder cannot accept inputs outside the training set

**Q114.** ○ *Single answer.* What does the VAE change about how each input is placed in the latent space, compared with a plain autoencoder?

- ○ **A.** Each input is mapped to one exact point, as before
- ○ **B.** Each input gets a Gaussian region, pulled toward the origin by the KL term
- ○ **C.** Inputs are sorted by class label
- ○ **D.** The decoder is replaced by a second encoder so that every input is stored twice, once on each side of the origin

**Q115.** ○ *Single answer.* What distribution does z follow when z_mean = 2.0 and z_log_var = log(0.25) ≈ −1.386?

```python
class Sampling(layers.Layer):
    def call(self, inputs):
        z_mean, z_log_var = inputs
        epsilon = K.random_normal(shape=tf.shape(z_mean))
        return z_mean + tf.exp(0.5 * z_log_var) * epsilon
```

- ○ **A.** N(−1.386, 2)
- ○ **B.** N(2, 0.25): mean 2, standard deviation 0.5
- ○ **C.** N(2, 0.25²)
- ○ **D.** N(0, 1), because ε is standard normal and the layer just passes the sampled noise through unchanged

**Q116.** ○ *Single answer.* What value does kl_loss take when the encoder outputs z_mean = 0 and z_log_var = 0 for every input?

```python
kl_loss = tf.reduce_mean(tf.reduce_sum(
    -0.5 * (1 + z_log_var - tf.square(z_mean) - tf.exp(z_log_var)), axis=1))
```

- ○ **A.** 0, because q(z|x) equals the prior N(0, I)
- ○ **B.** 1 per latent dimension, because the identity covariance contributes one unit of divergence for each dimension
- ○ **C.** −0.5
- ○ **D.** Infinity

**Q117.** ○ *Single answer.* In the KL line from the previous question, the student changes tf.reduce_sum(..., axis=1) to tf.reduce_mean(..., axis=1) with a 200-d latent. What is the effect?

```python
kl = tf.reduce_mean(tf.reduce_mean(            # was reduce_sum(..., axis=1)
    -0.5 * (1 + z_log_var - tf.square(z_mean) - tf.exp(z_log_var)), axis=1))
```

- ○ **A.** The KL term grows 200× and the posterior collapses, because averaging over dimensions amplifies each of them
- ○ **B.** It raises a shape error
- ○ **C.** None; sum and mean are equivalent inside a loss
- ○ **D.** The KL term shrinks 200×, so regularization is much weaker and the latent space less Gaussian

**Q118.** ○ *Single answer.* The decoder input is a 2-d vector, and shape_before_flattening = (4, 4, 128). What is the shape of decoder_output?

```python
x = layers.Dense(np.prod(shape_before_flattening))(decoder_input)
x = layers.Reshape(shape_before_flattening)(x)
x = layers.Conv2DTranspose(128, (3,3), strides=2, activation="relu", padding="same")(x)
x = layers.Conv2DTranspose(64,  (3,3), strides=2, activation="relu", padding="same")(x)
x = layers.Conv2DTranspose(32,  (3,3), strides=2, activation="relu", padding="same")(x)
decoder_output = layers.Conv2D(1, (3,3), strides=1, activation="sigmoid", padding="same")(x)
```

- ○ **A.** (None, 32, 32, 32), since the last transposed convolution has 32 filters and determines the channel count
- ○ **B.** (None, 2, 2, 1)
- ○ **C.** (None, 8, 8, 1)
- ○ **D.** (None, 32, 32, 1)

**Q119.** ○ *Single answer.* Why is x_train passed as both the input and the target?

```python
autoencoder = models.Model(encoder_input, decoder(encoder_output))
autoencoder.compile(optimizer="adam", loss="binary_crossentropy")
autoencoder.fit(x_train, x_train, epochs=5, batch_size=100, shuffle=True,
                validation_data=(x_test, x_test))
```

- ○ **A.** To double the effective batch size
- ○ **B.** The network is trained to reconstruct its own input through the bottleneck
- ○ **C.** Keras requires two copies of the data to compute gradients for the encoder and the decoder separately
- ○ **D.** It is a bug; labels y_train should be the target

**Q120.** ○ *Single answer.* What does this code produce when alpha runs from −3 to 3?

```python
smile_vec = z[smiling].mean(0) - z[~smiling].mean(0)
for alpha in np.linspace(-3, 3, 7):
    img = decoder.predict((z_face + alpha * smile_vec)[None])
```

- ○ **A.** An error, because alpha must be non-negative
- ○ **B.** The face goes from less to more smiling; negative alpha removes the smile
- ○ **C.** Faces of different people, since every step in latent space changes the identity
- ○ **D.** The same face with random noise added


### Answer key — Class 3 · Autoencoders & VAEs

**Q89 → A**

Latent variable models define a joint Pr(x, z) = Pr(x|z)Pr(z): a likelihood times a prior. For a discrete z (mixture of Gaussians) the integral becomes a sum Σ_n λ_n Norm(x; μ_n, σ_n²). For the nonlinear LVM, Pr(x|φ) = ∫ Norm(x; f[z, φ], σ²I) Norm(z; 0, I) dz, an infinite mixture of spherical Gaussians.

- A: ✓ Correct. Integrate the joint Pr(x, z) = Pr(x|z)Pr(z) over z.
- B: ✗ Taking a max gives a MAP-style approximation, not the marginal likelihood.
- C: ✗ Evaluating at one latent point ignores the prior and all other latents.
- D: ✗ This is a garbled Bayes’ rule. It contains Pr(x) on both sides and does not marginalize anything.

**Q90 → B, C, E**

With weights (0.7, 0.2, 0.1), the code below samples z, then x, and checks the histogram against Σ λ_n N(x; μ_n, σ_n²). Complexity grows with more components. The nonlinear latent variable model generalizes this to a continuous z and an infinite mixture.

- A: ✗ λ_n are probabilities: non-negative and summing to 1.
- B: ✓ Correct.
- C: ✓ Correct. This is marginalization over the discrete z.
- D: ✗ Mixing several Gaussians with different means produces multiple peaks. That is the whole point of a mixture.
- E: ✓ Correct.

**Q91 → D**

Because the marginal likelihood is an integral over a nonlinear network’s outputs, there is no closed-form expression and no easy way to evaluate it. The fix is a lower bound (the ELBO) that can be maximized with respect to both φ (decoder) and θ (variational/encoder parameters).

- A: ✗ Neural networks are differentiable. That is not the obstacle.
- B: ✗ In this model Pr(x|z) is Gaussian by construction.
- C: ✗ The prior is fixed to a standard normal Norm(0, I).
- D: ✓ Correct. This is why we introduce the ELBO.

**Q92 → B, C, D, E**

Optimization moves both between colored curves (improving θ tightens the bound) and along them (improving φ raises the likelihood). The VAE loss is the negative ELBO, minimized with SGD or Adam using automatic differentiation.

- A: ✗ Changing θ only changes the bound (moves between curves). The log-likelihood depends on φ alone.
- B: ✓ Correct. For fixed θ it is a function of φ alone (the colored curves).
- C: ✓ Correct, which is why it is called a lower bound.
- D: ✓ Correct. The gap is KL(q ‖ posterior).
- E: ✓ Correct. This is the reconstruction-minus-distance-to-prior view.

**Q93 → A, B, C**

KL(p ‖ q) = Σ p(x) log[p(x)/q(x)]. The zero-probability issue causes undefined or extreme gradients and can push q toward degenerate predictions. In the VAE, KL(q(z|x) ‖ N(0, I)) regularizes the latent space.

- A: ✓ Correct.
- B: ✓ Correct. KL(p‖q) contains the term p(x)·log(p(x)/0) = ∞.
- C: ✓ Correct.
- D: ✗ KL is asymmetric and violates the triangle inequality, so it is a divergence, not a metric.

**Q94 → B**

Per dimension, KL(N(μ, σ²) ‖ N(0, 1)) = ½(μ² + σ² − log σ² − 1). With log σ² = z_log_var this becomes −½(1 + z_log_var − μ² − e^{z_log_var}). It is zero when μ = 0 and σ = 1, which pulls encoded distributions toward the origin.

- A: ✗ This is not the Gaussian KL and ignores the variance term entirely.
- B: ✓ Correct. This is the analytic KL between a diagonal Gaussian and the standard normal.
- C: ✗ Not a KL divergence.
- D: ✗ Undefined for negative means and not a KL divergence.

**Q95 → C**

z_sigma = exp(z_log_var · 0.5). The encoder ignores covariance between latent dimensions, so it outputs only mean and log-variance vectors that define a diagonal multivariate normal.

- A: ✗ It does not. The KL term still depends on the variance.
- B: ✗ The encoder assumes zero correlation (diagonal covariance).
- C: ✓ Correct.
- D: ✗ The reparameterization trick needs σ, which is computed as exp(0.5 · log_var). There is no (0, 1) restriction.

**Q96 → B**

Sampling z ~ q(z|x) directly is non-differentiable with respect to the encoder parameters. Writing z = g(ε, x) with fixed-distribution noise turns it into a deterministic, differentiable transform, which makes backpropagation possible (Kingma & Welling, 2013).

- A: ✗ Randomness remains, but it is isolated in ε.
- B: ✓ Correct.
- C: ✗ The VAE encoder uses a diagonal covariance.
- D: ✗ Both the reconstruction and KL terms remain.

**Q97 → A, C, D**

Because nothing forces the latent space to be continuous, nearby points (e.g., (−2, 2) and (−2.1, 2.1)) need not decode to similar images, and sampling uniformly between min and max embeddings gives poor results. The VAE fixes this with neighborhood sampling plus the KL term.

- A: ✓ Correct (asymmetry).
- B: ✗ The opposite: gaps mean random samples often decode to poorly formed images.
- C: ✓ Correct (variable density).
- D: ✓ Correct (sparse gaps).

**Q98 → C**

Sampling around z_mean forces the decoder to produce similar images for nearby latent points, which gives continuity. The KL loss keeps those regions near the origin and limits their size, so there are fewer gaps. The decoder itself is identical to a plain autoencoder’s.

- A: ✗ VAEs are trained without labels.
- B: ✗ That is closer to GLO-style latent optimization.
- C: ✓ Correct.
- D: ✗ Transposed convolutions are in the decoder of both models.

**Q99 → C, D, E**

Loss = reconstruction loss + β · KL. The reconstruction term rewards fidelity, while the KL term regularizes toward the standard normal, giving a continuous, centered, gap-free latent space.

- A: ✗ Labels are never used. The VAE latent visualization shows each category roughly equally represented, with no preferential treatment.
- B: ✗ The KL term trades off against reconstruction and generally makes reconstructions blurrier.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✓ Correct.

**Q100 → B**

Faces are more complex than clothing, so they need more latent capacity (200 dimensions) and a stronger β to balance reconstruction against regularization. Batch normalization increases per-batch time but reduces the number of batches needed to converge.

- A: ✗ No GAN is involved, and the latent dimension was increased.
- B: ✓ Correct.
- C: ✗ All three are opposite to what was done.
- D: ✗ The encoder is still required.

**Q101 → B**

Labeled attributes (CelebA has 40) are used only after training to locate concept directions. The scalar α controls the strength of the change. Subtracting the vector removes the feature.

- A: ✗ No classifier weights are used.
- B: ✓ Correct. z_new = z + α · feature_vector.
- C: ✗ Features are not axis-aligned to a single known dimension.
- D: ✗ That is not arithmetic.

**Q102 → B**

Linear interpolation is meaningful only because the VAE latent space is continuous. In a plain AE, the straight line might cross empty gaps and decode to artifacts.

- A: ✗ No retraining is needed. Interpolation happens at inference time.
- B: ✓ Correct. Each intermediate point decodes to a new face.
- C: ✗ A continuous latent space yields gradual transitions.
- D: ✗ In a well-regularized VAE, interior points decode to plausible faces.

**Q103 → A**

For the nonlinear LVM, draw z* from the prior N(0, I), pass it through f[z*, φ] to get the mean of Pr(x|z*), then draw x*. Both distributions are normal, so this is straightforward. Diffusion models also generate this way, walking z_T → z_{T−1} → … → x.

- A: ✓ Correct.
- B: ✗ This goes against the factorization order.
- C: ✗ Gibbs sampling is a different (MCMC) method.
- D: ✗ That ignores the dependencies between variables.

**Q104 → B**

Transposed (fractionally strided) convolutions take a smaller spatial input with more channels and produce a larger output with fewer channels. The filter count sets the output channels. The decoder mirrors the encoder: Dense → Reshape → Conv2DTranspose stack → final Conv2D with sigmoid.

- A: ✗ Pooling downsamples and has no learnable kernel.
- B: ✓ Correct.
- C: ✗ That is what a stride-2 convolution does in the encoder.
- D: ✗ Attention is a different operation.

**Q105 → C**

With padding 'same' and stride 2, each conv halves height and width. Flatten has no parameters. Dense parameters = inputs × outputs + outputs (biases). The resulting 2-D latent space is what gets visualized.

- A: ✗ Each stride-2 layer halves the size once.
- B: ✗ This forgets the 2 bias terms.
- C: ✓ Correct. 32 → 16 → 8 → 4 spatially, with 128 channels.
- D: ✗ There are three stride-2 halvings: 32 → 16 → 8 → 4, not 8.

**Q106 → C**

autoencoder.compile(optimizer='adam', loss='binary_crossentropy'); fit(x_train, x_train, epochs=5, batch_size=100). The target equals the input because the network learns to reconstruct.

- A: ✗ There is no augmentation or latent comparison. The model is trained with x_train as both input and target.
- B: ✗ Hinge loss is for margin classifiers.
- C: ✓ Correct.
- D: ✗ The autoencoder reconstructs pixels and never uses the class labels.

**Q107 → A, C, D, E**

Components: a visual backbone (ImageNet-pretrained plus a conv neck); a frozen VGGish audio encoder (AudioSet); three latent encoders φ_sv, φ_sa, φ_c; and a decoder with TPAVI cross-modal attention producing pixel-wise masks. The objective is the ELBO (reconstruction plus KL) with the extra constraints. On AVSBench it gains +3.00 and +3.84 mIoU on the S4 and MS3 settings (PVTv2 backbone).

- A: ✓ Correct.
- B: ✗ This is the limitation ECMVAE fixes. It explicitly models each modality’s contribution.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✓ Correct.

**Q108 → B**

Audio provides category information. Visual identifies candidate sound producers in the scene. The shared code corresponds to the actual target sound producers. Cross-modal learning is what makes AVS possible.

- A: ✗ That describes the visual modality.
- B: ✓ Correct.
- C: ✗ Audio carries critical category information.
- D: ✗ Localization comes mainly from the visual modality, combined with shared information.

**Q109 → D**

AVSBench has 5,356 video sequences with audio and binary per-pixel annotations. mIoU measures mask overlap; F-score combines precision and recall.

- A: ✗ Not clip lengths.
- B: ✗ The metrics are mIoU and F-score.
- C: ✗ Not training-regime labels.
- D: ✓ Correct.

**Q110 → B**

z is lower-dimensional than x, so f captures the important factors. Pr(x|φ) is an infinite mixture of spherical Gaussians weighted by Pr(z).

- A: ✗ This is reversed.
- B: ✓ Correct.
- C: ✗ In this model it is a spherical (shared) variance, assumed known.
- D: ✗ z carries the structure through f.

**Q111 → C**

Hence the variational approximation q(z|x, θ) = N(g_μ[x, θ], g_Σ[x, θ]) with a diagonal covariance, found by minimizing KL to the true posterior. That is equivalent to maximizing the ELBO.

- A: ✗ The true posterior is generally complex and non-Gaussian.
- B: ✗ The prior is the fixed standard normal.
- C: ✓ Correct.
- D: ✗ The likelihood is differentiable.

**Q112 → A, C, D**

A general multivariate normal N(μ, Σ) has a mean vector and a symmetric covariance matrix. The VAE prior is N(0, I) and the encoder outputs a diagonal Σ.

- A: ✓ Correct.
- B: ✗ Covariance matrices are always symmetric.
- C: ✓ Correct.
- D: ✓ Correct.

**Q113 → C**

There is no requirement for the latent space to be continuous, and it is uneven and asymmetric. VAEs add sampling around each mean and a KL penalty, which turns the autoencoder into a strong generative model.

- A: ✗ An autoencoder has a decoder.
- B: ✗ A plain AE encoder is deterministic.
- C: ✓ Correct.
- D: ✗ The decoder accepts any vector.

**Q114 → B**

Encoding to areas gives more diversity and avoids discontinuities. The constraints are the KL term: center the areas, limit their size, and penalize deviation.

- A: ✗ That is the plain autoencoder.
- B: ✓ Correct.
- C: ✗ No such mechanism exists in a VAE.
- D: ✗ No such mechanism exists in a VAE.

**Q115 → B**

z = μ + σ·ε with σ = exp(½·log σ²). Because ε is sampled outside the computation graph, gradients reach z_mean and z_log_var. That is the reparameterization trick.

- A: ✗ Mean and log-variance are swapped here.
- B: ✓ Correct.
- C: ✗ exp(0.5 · log 0.25) = 0.5 is the standard deviation, so the variance is 0.25, not 0.25².
- D: ✗ The noise is shifted by z_mean and scaled by σ.

**Q116 → A**

Per dimension: −½(1 + log σ² − μ² − σ²). At μ = 0, σ = 1 this is 0. If the KL term dominates (large β), the encoder is pushed toward exactly this output, which is posterior collapse.

- A: ✓ Correct. The encoder then carries no information about x.
- B: ✗ The terms cancel to 0.
- C: ✗ Inside the sum each term is 1 + 0 − 0 − 1 = 0.
- D: ✗ No.

**Q117 → D**

The KL of a diagonal Gaussian is a sum over dimensions. Averaging silently reweights it relative to the reconstruction term, which works like changing β. This kind of bug is easy to miss when reading code.

- A: ✗ Averaging divides the term. It does not multiply it.
- B: ✗ Both reduce axis 1 and give the same shape.
- C: ✗ They differ by a factor equal to the latent size.
- D: ✓ Correct.

**Q118 → D**

Dense(2,048) → Reshape(4, 4, 128) → three Conv2DTranspose layers with stride 2 → Conv2D(1, sigmoid). The decoder mirrors the encoder, so the output matches the 32×32×1 input.

- A: ✗ The final Conv2D(1, …) maps to one channel.
- B: ✗ Transposed stride-2 convolutions upsample. They do not downsample.
- C: ✗ There are three stride-2 transposed convolutions, not one.
- D: ✓ Correct. 4 → 8 → 16 → 32, then Conv2D(1) sets one channel.

**Q119 → B**

The loss compares the decoder output with the input itself. Learning a good 2-d code is a side effect of having to squeeze the image through the bottleneck.

- A: ✗ The batch size is set by batch_size.
- B: ✓ Correct. It is unsupervised.
- C: ✗ No such requirement exists.
- D: ✗ Autoencoders need no labels.

**Q120 → B**

smile_vec = mean(z of smiling faces) − mean(z of non-smiling faces), computed using CelebA attribute labels after training. This only works because the VAE latent space is continuous and roughly linear in attributes.

- A: ✗ Negative values are valid. They subtract the feature.
- B: ✓ Correct.
- C: ✗ Moving along an attribute direction mostly keeps the identity.
- D: ✗ Nothing random is added. The shift is along a fixed direction.


---

## Class 4 · Transformers

**Q121.** ○ *Single answer.* In scaled dot-product attention, Attention(Q, K, V) = softmax(QKᵀ / √d_k) V. Why divide by √d_k?

- ○ **A.** To reduce the number of parameters in W_Q and W_K
- ○ **B.** To make the attention weights sum to 1 across each row before the values are aggregated
- ○ **C.** Because additive attention requires it to remain numerically equivalent to multiplicative attention for any key dimension
- ○ **D.** Large d_k makes dot products large, pushing softmax into regions with tiny gradients; scaling counteracts this

**Q122.** ☐ *Select all that apply.* Which statements about queries, keys and values are correct? Select all that apply.

- ☐ **A.** Attention is a soft lookup: queries match all keys with weights in [0, 1]
- ☐ **B.** V holds per-position weights, and K holds the content that is ultimately summed into the output vector for each token
- ☐ **C.** Q, K and V are computed as XW_Q, XW_K and XW_V, where the W matrices are the learnable parameters
- ☐ **D.** Each query attends only to the single key with the highest score, and the other values are discarded
- ☐ **E.** The attention weight matrix softmax(QKᵀ/√d_k) has shape (n, n) for a sequence of length n

**Q123.** ○ *Single answer.* Why do Transformers need positional encodings?

- ○ **A.** To prevent the decoder from attending to future tokens
- ○ **B.** To reduce the memory cost of attention from quadratic to linear in sequence length
- ○ **C.** Self-attention has no recurrence or convolution, so it is permutation-invariant and order must be injected
- ○ **D.** Because word embeddings are too small to hold semantic content, so extra dimensions with position data are needed

**Q124.** ☐ *Select all that apply.* Which statements about multi-head attention are correct? Select all that apply.

- ☐ **A.** Different heads can track different relations, e.g., long-distance dependencies or anaphora
- ☐ **B.** Head outputs are concatenated and projected by a final matrix W_O
- ☐ **C.** All heads share one set of projection weights, so multiple heads only average out the noise in the attention scores
- ☐ **D.** Each head has its own W_Q, W_K, W_V, so heads can learn distinct attention patterns

**Q125.** ○ *Single answer.* What does the causal (look-ahead) mask do in decoder self-attention?

- ○ **A.** It masks out padding tokens only, leaving all real tokens visible in both directions so that the context is bidirectional
- ○ **B.** It sets scores for future positions to −∞ before softmax, so each token sees only earlier ones
- ○ **C.** It hides the encoder output from the decoder so that the model cannot copy the source sentence
- ○ **D.** It randomly drops 15% of tokens, as in BERT pretraining

**Q126.** ○ *Single answer.* In encoder–decoder cross-attention, where do Q, K and V come from?

- ○ **A.** Q from the previous decoder layer; K and V from the encoder output
- ○ **B.** Q, K and V all come from the encoder output, which is computed once and reused at each step
- ○ **C.** Q, K and V all come from the decoder’s own previous layer, as in self-attention
- ○ **D.** Q from the encoder output; K and V from the decoder layer below, so the encoder decides which decoded tokens matter

**Q127.** ☐ *Select all that apply.* Match Transformer families to their descriptions. Which pairings are correct? Select all that apply.

- ☐ **A.** Encoder-only models use causal masking and are therefore the natural first choice for open-ended, token-by-token text generation
- ☐ **B.** Encoder–decoder (T5, BART): maps one text sequence to another, e.g., translation and summarization
- ☐ **C.** Encoder-only (BERT, RoBERTa): bidirectional context; suited to classification and NER
- ☐ **D.** Decoder-only (GPT): left context only; generates by next-token prediction

**Q128.** ☐ *Select all that apply.* Which statements about BERT pretraining are correct? Select all that apply.

- ☐ **A.** MLM predicts masked tokens’ original ids using left and right context
- ☐ **B.** The input embedding is the sum of token, segment and position embeddings
- ☐ **C.** Pretraining data is BooksCorpus (800M words) plus English Wikipedia (2,500M words)
- ☐ **D.** In NSP, B is the true next sentence 50% of the time and random otherwise
- ☐ **E.** BERT-Large has 12 layers, hidden size 768 and 12 heads, for a total of roughly 110 million parameters

**Q129.** ○ *Single answer.* Which statement best describes T5 (Text-to-Text Transfer Transformer)?

- ○ **A.** An encoder-only model that outputs class probabilities
- ○ **B.** Every task is cast as text in, text out, with one encoder–decoder model
- ○ **C.** A vision–language model that converts images to captions by treating pixels as text tokens
- ○ **D.** A decoder-only model trained exclusively on code, which is later prompted with natural-language instructions

**Q130.** ☐ *Select all that apply.* Layer normalization in the Transformer. Which statements are correct? Select all that apply.

- ☐ **A.** For an input of shape [N, C, H, W], it computes statistics over [C, H, W] for each sample
- ☐ **B.** It normalizes each sample’s activations to zero mean and unit variance, independently per training case
- ☐ **C.** It computes the mean and variance across the batch dimension, so its behavior changes with batch size, like batch norm
- ☐ **D.** After normalization it applies learnable scale γ and shift β

**Q131.** ○ *Single answer.* According to Geva et al. (2020), what are Transformer feed-forward layers?

- ○ **A.** Redundant layers that can be removed without changing predictions, since attention alone determines the next token
- ○ **B.** Gating mechanisms equivalent to LSTM forget gates
- ○ **C.** Purely positional encoders that recompute each token’s position after every attention block
- ○ **D.** Key–value memories: keys detect input patterns, and values induce distributions over the output vocabulary

**Q132.** ☐ *Select all that apply.* Causal mediation analysis applied to neural networks. Which statements are correct? Select all that apply.

- ☐ **A.** Mediators are internal states such as neurons, layers or attention heads
- ☐ **B.** The independent variable is typically the model input and the dependent variable the model output
- ☐ **C.** The indirect effect is the part of the total effect that passes through the mediator
- ☐ **D.** The direct effect is measured by changing the mediator while holding the model input completely fixed

**Q133.** ☐ *Select all that apply.* MEMIT (Mass-Editing Memory in a Transformer). Which statements are correct? Select all that apply.

- ☐ **A.** Its goals include effectiveness, generalization to paraphrases, specificity and fluency
- ☐ **B.** It uses causal analysis to locate critical MLP layers on the factual-recall path and edits them
- ☐ **C.** It updates knowledge by retraining the whole model from scratch on a corrected corpus that contains the new facts
- ☐ **D.** It was validated on GPT-J and GPT-NeoX
- ☐ **E.** It inserts thousands of factual memories directly into the model weights in a batch

**Q134.** ○ *Single answer.* T-DMCA (Liu et al., 2018) modifies decoder self-attention for long sequences. What do its two components do?

- ○ **A.** Local attention removes the softmax, and memory-compressed attention removes positional encodings
- ○ **B.** Local attention uses blocks; memory-compressed attention shrinks K and V by strided conv
- ○ **C.** It replaces attention with an LSTM
- ○ **D.** Both components compress the queries, while keys and values stay at full length so no information is lost

**Q135.** ○ *Single answer.* Why does attention help with long-range dependencies compared to an RNN?

- ○ **A.** Any two positions connect directly, so gradients need not cross many time steps
- ○ **B.** It stores the entire past in a single fixed-size hidden vector, just as an RNN does but at a higher dimension
- ○ **C.** It removes the need for any training data
- ○ **D.** It uses fewer floating-point operations for every sequence length

**Q136.** ○ *Single answer.* He et al. (2016) describe a degradation problem in deep plain networks. What is it?

- ○ **A.** Images degrade after many convolutions because each filter blurs the signal a little more
- ○ **B.** Test error increases because of overfitting
- ○ **C.** Weights decay toward zero because of L2 regularization, which shrinks the effective capacity of every additional layer
- ○ **D.** Training error increases with depth even though a deeper network has more capacity

**Q137.** ○ *Single answer.* Additive attention and dot-product attention compared. Which statement matches Vaswani et al.?

- ○ **A.** Additive attention has no learnable parameters, which is why it is faster to train
- ○ **B.** Additive attention is much faster in practice
- ○ **C.** Dot-product attention always outperforms additive attention, with or without scaling, for every d_k
- ○ **D.** Similar complexity, but dot-product is faster and more memory-efficient

**Q138.** ○ *Single answer.* In GPT (Radford et al., 2018), how is the pretrained model adapted to downstream tasks?

- ○ **A.** By freezing all weights and using k-nearest neighbors on embeddings
- ○ **B.** By replacing the decoder with a BERT-style bidirectional encoder before fine-tuning on the labeled task data
- ○ **C.** By training a new model from scratch for each task
- ○ **D.** Supervised fine-tuning with task-specific input transformations and a new output layer

**Q139.** ○ *Single answer.* Pretraining a language model before fine-tuning adds an inductive bias. What does that mean here?

- ○ **A.** The model is biased toward the majority class
- ○ **B.** Language knowledge is preloaded, so it generalizes better with little task data
- ○ **C.** The model’s weights are randomly initialized for each task
- ○ **D.** The architecture is constrained to use convolutions, so that it is biased toward local patterns in text

**Q140.** ○ *Single answer.* For BERT-Base (H = 768, A = 12), what is the dimension of each attention head?

- ○ **A.** 64
- ○ **B.** 1,024
- ○ **C.** 768
- ○ **D.** 12, because each head works with one dimension per layer, and BERT-Base has twelve layers

**Q141.** ○ *Single answer.* For a sequence of n tokens, how do the memory and compute of the self-attention score matrix scale?

- ○ **A.** O(n²)
- ○ **B.** O(1)
- ○ **C.** O(n)
- ○ **D.** O(log n), because softmax normalizes each row and so only a few entries ever need to be stored

**Q142.** ☐ *Select all that apply.* Which statements about the sinusoidal positional encoding are correct? Select all that apply.

- ☐ **A.** The encoding is learned by backpropagation together with the token embeddings during pretraining
- ☐ **B.** PE_{pos+k} is a linear function of PE_pos for any fixed offset k
- ☐ **C.** The wavelengths form a geometric progression from 2π to 10000·2π
- ☐ **D.** Each dimension corresponds to a sinusoid of a different frequency

**Q143.** ○ *Single answer.* In causal mediation analysis, how is the direct effect estimated?

- ○ **A.** Vary the input while holding the mediator fixed
- ○ **B.** Remove the output layer
- ○ **C.** Clamp the input and change only the mediator, measuring how far the output moves
- ○ **D.** Vary the input and let all mediators change freely

**Q144.** ☐ *Select all that apply.* Which factual-recall mechanism did MEMIT’s causal analysis find? Select all that apply.

- ☐ **A.** MLPs in a range of critical layers read this and write memories into the residual stream
- ☐ **B.** Facts are stored only in the final softmax layer’s bias vector, which MEMIT overwrites for each new fact
- ☐ **C.** Early-layer attention gathers the subject into the last subject token
- ☐ **D.** Later attention reads these hidden states to produce the output

**Q145.** ○ *Single answer.* Which MEMIT editing criterion is about not disturbing unrelated facts?

- ○ **A.** Generalization, which checks that the new fact is recalled under many different phrasings
- ○ **B.** Specificity
- ○ **C.** Effectiveness
- ○ **D.** Fluency

**Q146.** ○ *Single answer.* During GPT-style training, a student forgets to apply the causal mask. Training loss drops much faster than usual. What happens at generation time?

- ○ **A.** Generation becomes faster because each step can skip computing the full attention matrix over previous tokens
- ○ **B.** Nothing changes, because positional encodings already enforce ordering
- ○ **C.** Generation works better because the model learned bidirectional context
- ○ **D.** Quality collapses: training let it read the next token, a shortcut that is absent at generation

**Q147.** ○ *Single answer.* An attention layer uses d_k = 1024 and the student removes the 1/√d_k scaling. What is the most likely training symptom?

- ○ **A.** Attention rows no longer sum to 1
- ○ **B.** Near one-hot attention with tiny gradients, so training stalls
- ○ **C.** Attention becomes uniform over all positions
- ○ **D.** The attention matrix changes shape from (n, n) to (n, d_k), which breaks the matrix multiplication with V

**Q148.** ○ *Single answer.* A Transformer encoder is trained with no positional encoding at all. You feed it “dog bites man” and “man bites dog”. What do you observe?

- ○ **A.** Outputs that are all identical vectors
- ○ **B.** The same set of output vectors, just permuted, so the two sentences cannot be told apart
- ○ **C.** A runtime error, since the attention layer requires a position embedding as a mandatory input to compute keys
- ○ **D.** Different outputs, because attention weights depend on word order

**Q149.** ○ *Single answer.* A student replaces “concatenate heads, then multiply by W_O” with “average the head outputs”. What is lost?

- ○ **A.** Nothing; averaging and W_O are equivalent
- ○ **B.** The causal mask
- ○ **C.** The softmax normalization inside each head, which only works when the heads are concatenated afterward
- ○ **D.** The learned mixing of head subspaces; each head’s output also shrinks to d_model/h dimensions

**Q150.** ☐ *Select all that apply.* A BERT-style encoder and a GPT-style decoder each process “the bank by the river”. Which statements are correct? Select all that apply.

- ☐ **A.** In GPT, the representation of “bank” cannot use “river”, because it comes later
- ☐ **B.** In BERT, the representation of “bank” can use the word “river”
- ☐ **C.** GPT’s attention weight matrix is lower-triangular
- ☐ **D.** BERT’s attention matrix is always symmetric, since every token attends to every other token equally

**Q151.** ○ *Single answer.* Q, K and V have shape (batch = 2, heads = 8, seq = 10, d_k = 64). What is the shape of weights, and of output?

```python
scores = tf.matmul(Q, K, transpose_b=True) / tf.math.sqrt(tf.cast(d_k, tf.float32))
weights = tf.nn.softmax(scores, axis=-1)
output = tf.matmul(weights, V)
```

- ○ **A.** weights (2, 8, 64, 64); output (2, 8, 10, 64)
- ○ **B.** weights (2, 10, 10); output (2, 10, 64), because heads are summed before the softmax
- ○ **C.** weights (2, 8, 10, 10); output (2, 8, 10, 10), because the output keeps the shape of the attention matrix
- ○ **D.** weights (2, 8, 10, 10); output (2, 8, 10, 64)

**Q152.** ○ *Single answer.* What does this mask allow, and where is it used?

```python
n = tf.shape(x)[1]
mask = tf.linalg.band_part(tf.ones((n, n)), -1, 0)   # lower triangle of 1s
scores = scores + (1.0 - mask) * -1e9
```

- ○ **A.** It masks padding tokens
- ○ **B.** Token i attends to positions j ≤ i; a causal mask for GPT-style decoders
- ○ **C.** Each token may attend to future tokens only; used in BERT
- ○ **D.** Each token attends only to itself, which is used to stop information leaking between positions in an encoder

**Q153.** ○ *Single answer.* In this sinusoidal positional-encoding code, what is true about the columns of pe?

```python
pos = np.arange(max_len)[:, None]
i = np.arange(0, d_model, 2)[None, :]
angle = pos / np.power(10000, i / d_model)
pe = np.zeros((max_len, d_model))
pe[:, 0::2] = np.sin(angle)
pe[:, 1::2] = np.cos(angle)
```

- ○ **A.** Even columns are sin, odd are cos, frequency falling with column index
- ○ **B.** The values are learned during training, so they differ between models trained on different data
- ○ **C.** Every column has the same frequency
- ○ **D.** Values grow without bound with position

**Q154.** ○ *Single answer.* In Keras MultiHeadAttention(num_heads=2, key_dim=256) applied to 256-d inputs, what is key_dim?

```python
attn = layers.MultiHeadAttention(num_heads=2, key_dim=256, output_shape=256)
out = attn(x, x, attention_mask=causal_mask)     # x: (batch, seq, 256)
```

- ○ **A.** The total model width, split across the 2 heads (128 each)
- ○ **B.** The number of tokens the layer can attend to, so longer sequences raise an error at runtime
- ○ **C.** The vocabulary size
- ○ **D.** The per-head size: each head projects to 256-d Q and K, 512 total

**Q155.** ○ *Single answer.* Which arrangement does this Transformer block use, and what are the two `+` operations?

```python
attn_out = self.attn(x, x, attention_mask=mask)
out1 = self.ln_1(x + self.dropout_1(attn_out))
ffn_out = self.ffn_2(self.ffn_1(out1))
return self.ln_2(out1 + self.dropout_2(ffn_out))
```

- ○ **A.** Pre-LN; the + operations concatenate features
- ○ **B.** Post-LN: LayerNorm(x + Sublayer(x)), with residuals around attention and the FFN
- ○ **C.** There are no residual connections; + adds the positional encodings back in before each sub-layer
- ○ **D.** Batch normalization with skip connections

**Q156.** ○ *Single answer.* For bert-base-uncased, what does this code print?

```python
tok = AutoTokenizer.from_pretrained("bert-base-uncased")
ids = tok("Hello world")["input_ids"]
print(tok.convert_ids_to_tokens(ids))
```

- ○ **A.** ['hello', 'world']
- ○ **B.** ['hel', '##lo', 'wor', '##ld']
- ○ **C.** ['[CLS]', 'hello', 'world', '[SEP]']
- ○ **D.** ['[CLS]', 'Hello', 'world', '[SEP]'], since an uncased tokenizer still keeps the original capitalization

**Q157.** ○ *Single answer.* bert-base has 12 layers and 12 heads. What is len(out.attentions), and what is the shape of out.attentions[0] for a 15-token input?

```python
out = model(**inputs, output_attentions=True)
print(len(out.attentions), out.attentions[0].shape)
```

- ○ **A.** 144, one tensor per head, each of shape (15, 15), returned as a flat list over layers and heads
- ○ **B.** 12; (1, 12, 15, 15): batch, heads, query, key
- ○ **C.** 12; (1, 15, 15)
- ○ **D.** 1; (12, 12, 15, 15)


### Answer key — Class 4 · Transformers

**Q121 → D**

If q and k have components with zero mean and unit variance, q·k has variance d_k. Large-magnitude logits saturate the softmax into near one-hot outputs with near-zero gradients. Vaswani et al. note that unscaled dot-product attention is outperformed by additive attention at large d_k. Dot-product attention is preferred because it is faster and more space-efficient via optimized matrix multiplication.

- A: ✗ Scaling is a constant, so it has no effect on the parameter count.
- B: ✗ The softmax already normalizes rows to sum to 1.
- C: ✗ Additive attention uses a feed-forward network. Scaling is what fixes dot-product attention at large d_k.
- D: ✓ Correct.

**Q122 → A, C, E**

The query is the representation of the current task (“what word follows ‘too’?”). Keys describe which prediction tasks each word can help with. Values are each word’s unweighted contribution. Output Z = weights · V with shape (n, d_v).

- A: ✓ Correct. This is John Hewitt’s “fuzzy key-value store” view.
- B: ✗ Roles are swapped. Values are the content that is summed; keys are matched against queries.
- C: ✓ Correct. The attention arithmetic itself has no parameters.
- D: ✗ That would be hard attention. Softmax gives a weighted average over all values.
- E: ✓ Correct.

**Q123 → C**

The original Transformer adds sinusoidal encodings PE(pos, 2i) = sin(pos / 10000^{2i/d_model}) and PE(pos, 2i+1) = cos(·) to the token embeddings. The wavelengths form a geometric progression from 2π to 10000·2π, and PE_{pos+k} is a linear function of PE_pos, which helps the model attend by relative position.

- A: ✗ That is the job of the causal mask.
- B: ✗ Positional encodings do not change memory complexity.
- C: ✓ Correct.
- D: ✗ Positional encodings are added element-wise in the same dimension. They add no extra dimensions.

**Q124 → A, B, D**

BERT-Base has L = 12, H = 768 and A = 12 heads, so each head works in a 64-dimensional subspace (768/12).

- A: ✓ Correct. Vaswani et al. visualize layer-5 heads tracking “making … more difficult” and resolving “its.”
- B: ✓ Correct.
- C: ✗ Heads have separate projections. Averaging identical heads would add nothing.
- D: ✓ Correct.

**Q125 → B**

Masking enforces the autoregressive property: p(x_t | x_<t). The model cannot peek at the future, and training is still parallel across positions because the whole masked matrix is computed in one pass.

- A: ✗ Padding masks exist, but the causal mask specifically blocks future positions.
- B: ✓ Correct.
- C: ✗ Cross-attention explicitly uses the encoder output.
- D: ✗ That is MLM masking of inputs, not attention masking.

**Q126 → A**

Cross-attention is regular dot-product attention across two sequences. Each decoder token decides which encoded input tokens are most relevant to the next prediction, which is how translation and summarization models (T5, BART) connect input meaning to output.

- A: ✓ Correct.
- B: ✗ Then the decoder state would not influence what is retrieved.
- C: ✗ That is decoder self-attention.
- D: ✗ This is reversed. The decoder asks the questions (queries).

**Q127 → B, C, D**

The distinction comes from the attention mask. No mask gives bidirectional context (encoder). A causal mask gives left-to-right context (decoder). Cross-attention connects the two. The lines blur in practice: GPT-style models can be prompted to translate, and BERT can be applied to summarization. A decoder-only model drops the encoder stack, roughly halving the parameters of a comparable encoder–decoder.

- A: ✗ Encoder-only models use unmasked (bidirectional) attention.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.

**Q128 → A, B, C, D**

The same architecture is used for pretraining and fine-tuning, and the pretrained parameters initialize every downstream task (SQuAD, SWAG, MRPC, …). A pre-trained encoder alone struggles with generation, e.g., filling “George Washington [MASK] the Delaware” only as a single-token cloze task.

- A: ✓ Correct. This is what makes deep bidirectional pretraining possible.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✗ Those are BERT-Base numbers. Large is L = 24, H = 1024, A = 16, about 340M parameters.

**Q129 → B**

Raffel et al. (2020): a unified text-to-text format means one model, one loss, and one decoding procedure for every task. For classification the model simply generates the label word.

- A: ✗ T5 is encoder–decoder and outputs text.
- B: ✓ Correct.
- C: ✗ T5 is a text model.
- D: ✗ Not T5.

**Q130 → A, B, D**

Layer norm (Ba et al., 2016) standardizes sub-layer inputs, stabilizes hidden-state dynamics, regulates scale, and speeds convergence. In the pre-LN arrangement (used in ViT and GPT-2), it is applied before multi-head attention and the feed-forward network, with residual connections around each.

- A: ✓ Correct.
- B: ✓ Correct. It does not depend on other samples in the batch.
- C: ✗ That describes batch normalization.
- D: ✓ Correct.

**Q131 → D**

Lower layers capture shallow patterns (e.g., common suffixes, n-grams); upper layers capture semantic themes. For example, “interest rates” triggers a key whose value predicts “increase” or “decrease”, and “despite the rain” predicts “we”, “they” or “the event”. Outputs are aggregated through residual connections and refined layer by layer.

- A: ✗ FFN layers hold most parameters and store factual and linguistic associations.
- B: ✗ Not equivalent.
- C: ✗ They store content associations, not position.
- D: ✓ Correct.

**Q132 → A, B, C**

Steps: set up the model; estimate total, direct and indirect effects; intervene (e.g., clamp neurons) to confirm causal roles; test significance. In LLMs this identified which MLP layers mediate factual recall, which is the basis of ROME and MEMIT.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✗ The direct effect varies the input while holding the mediator fixed.

**Q133 → A, B, D, E**

Mechanism: early-layer attention gathers the subject into the last subject token; critical MLPs read it and write memories into the residual stream; later attention reads them out. MEMIT stores new key→value associations in those MLPs, focusing on the last subject token. Examples of the problem: “Arneb is in Aquila” (wrong; it is Lepus) and “Vice President is Mike Pence” (out of date).

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✗ Avoiding full retraining is the motivation. Retraining is resource-intensive and impractical.
- D: ✓ Correct.
- E: ✓ Correct. Earlier methods handled one or a few edits.

**Q134 → B**

Local layers handle micro-context with constant memory per block; memory-compressed layers exchange global information without the full quadratic memory cost. Together they let the decoder summarize long inputs (the Wikipedia generation task).

- A: ✗ Neither is removed.
- B: ✓ Correct. The convolution has kernel 3 and stride 3; queries are unchanged.
- C: ✗ It stays attention-based.
- D: ✗ Memory-compressed attention reduces keys and values, not queries.

**Q135 → A**

RNNs multiply many Jacobians over time, so gradients usually vanish and occasionally explode. Attention filters context dynamically, retrieves only relevant parts, and avoids keeping irrelevant history.

- A: ✓ Correct.
- B: ✗ That is the RNN bottleneck attention avoids.
- C: ✗ No.
- D: ✗ Attention is O(n²) in sequence length, which is more expensive for long sequences.

**Q136 → D**

Solvers struggle to fit identity mappings with stacked nonlinear layers. Residual learning fits F(x) = H(x) − x and outputs F(x) + x, so F = 0 recovers identity. The same residual idea appears in Transformers, PixelCNN and the diffusion U-Net.

- A: ✗ Not what “degradation” means here.
- B: ✗ Training error also rises, so this is not overfitting.
- C: ✗ Not the described cause.
- D: ✓ Correct. It is an optimization problem, not overfitting.

**Q137 → D**

Additive attention computes compatibility with a small MLP. Dot-product attention computes QKᵀ, which is efficient on GPUs. Scaling by 1/√d_k fixes dot-product attention’s weakness at large d_k.

- A: ✗ It uses a single-hidden-layer feed-forward network, which has parameters.
- B: ✗ Dot-product attention is faster thanks to optimized matrix multiplication.
- C: ✗ Unscaled dot-product attention loses to additive attention at large d_k.
- D: ✓ Correct.

**Q138 → D**

GPT is semi-supervised: unsupervised language-model pretraining on a large corpus, then supervised fine-tuning. Tasks such as entailment or multiple choice are converted into token sequences with delimiter tokens, with minimal changes to the architecture.

- A: ✗ Not the GPT recipe.
- B: ✗ GPT keeps its decoder-only architecture.
- C: ✗ That would discard the pretrained knowledge.
- D: ✓ Correct.

**Q139 → B**

Pretraining on large unlabeled corpora (BooksCorpus, Wikipedia) teaches general regularities of language by predicting tokens in context. The result is a general-purpose model ready for fine-tuning.

- A: ✗ Inductive bias here means useful prior knowledge, not class imbalance.
- B: ✓ Correct.
- C: ✗ Pretraining does the opposite.
- D: ✗ Pretraining does not change the architecture.

**Q140 → A**

Multi-head attention splits d_model across heads, then concatenates them and projects with W_O, so total cost is similar to one full-width head.

- A: ✓ Correct. 768 / 12.
- B: ✗ That is BERT-Large’s hidden size.
- C: ✗ That is the full hidden size, shared across heads.
- D: ✗ That confuses heads with layers.

**Q141 → A**

This quadratic cost motivates T-DMCA (local plus memory-compressed attention), GPT-3’s sparse attention and ViT’s patching.

- A: ✓ Correct.
- B: ✗ No.
- C: ✗ Every token is compared with every other token.
- D: ✗ All n² scores are computed.

**Q142 → B, C, D**

PE(pos, 2i) = sin(pos/10000^{2i/d_model}) and PE(pos, 2i+1) = cos(…). They are added element-wise to the token embeddings.

- A: ✗ Sinusoidal encodings are fixed. Learned embeddings (BERT, ViT) are a different option.
- B: ✓ Correct. This helps the model attend by relative position.
- C: ✓ Correct.
- D: ✓ Correct.

**Q143 → A**

Total = observe output change when input varies. Direct = vary input with the mediator fixed. Indirect = the effect transmitted through the mediator.

- A: ✓ Correct.
- B: ✗ Not part of the method.
- C: ✗ That isolates the mediator’s own effect, which relates to the indirect path.
- D: ✗ That gives the total effect.

**Q144 → A, C, D**

MEMIT edits by storing new key→value vector associations in those critical MLPs, spreading each update over several layers for scale.

- A: ✓ Correct.
- B: ✗ Facts are mediated by mid-layer MLPs.
- C: ✓ Correct.
- D: ✓ Correct.

**Q145 → B**

The four criteria: effectiveness, generalization, specificity and fluency.

- A: ✗ That is paraphrase robustness.
- B: ✓ Correct.
- C: ✗ Effectiveness means the new fact wins over the old one.
- D: ✗ Fluency is about natural post-edit text.

**Q146 → D**

With teacher forcing, the input at position t+1 is the target at position t. Without the mask, the attention at t can read that input and copy it, so the loss falls toward 0. At inference, position t+1 is empty until the model predicts it, so the copying strategy fails. This mismatch is a classic data leak.

- A: ✗ Speed is unrelated. The mask changes what the model learns.
- B: ✗ Positional encodings say where a token is. They do not stop attention from reading the future.
- C: ✗ At generation the future tokens do not exist yet, so the model cannot use what it learned.
- D: ✓ Correct. The low loss came from a leak, not from learning.

**Q147 → B**

Var(q·k) ≈ d_k for unit-variance components, so the standard deviation is 32 at d_k = 1024. The softmax of such logits is essentially an argmax, whose Jacobian is nearly 0. The ‘Why divide by √d_k’ code panel shows the maximum weight going from 0.29 (scaled) to 1.00 (raw) at d_k = 512.

- A: ✗ Softmax always makes rows sum to 1, scaled or not.
- B: ✓ Correct. Logit variance grows to about 1,024, which saturates the softmax.
- C: ✗ The opposite. Large logits make attention extremely peaked.
- D: ✗ Scaling multiplies by a constant. Shapes are unchanged.

**Q148 → B**

Permuting the rows of X permutes Q, K and V the same way. The weight matrix gets its rows and columns permuted, so each output row is the same vector at a new index. Pooling over tokens (e.g., a mean) would then give identical sentence embeddings. An RNN does not have this problem, because it reads tokens in order.

- A: ✗ Different words still get different vectors.
- B: ✓ Correct. Self-attention is permutation-equivariant.
- C: ✗ It runs fine, but it is blind to order.
- D: ✗ Without positions, attention depends only on content, and the content here is identical.

**Q149 → D**

Concatenating gives an (n, h·d_head) matrix, and W_O learns how to combine the heads. Averaging forces equal weights and drops the dimensional layout, so the model cannot route ‘syntax-head’ and ‘coreference-head’ information to different output features.

- A: ✗ Averaging is one fixed, specific choice of W_O.
- B: ✗ Masking is separate from how heads are combined.
- C: ✗ The softmax happens inside each head and is unaffected.
- D: ✓ Correct.

**Q150 → A, B, C**

This is why BERT is strong at understanding tasks such as disambiguation and NER, and GPT is natural for generation. In GPT, “bank” can only be disambiguated by tokens after it, inside those later tokens’ own representations.

- A: ✓ Correct. The causal mask blocks future tokens.
- B: ✓ Correct. Encoder attention is bidirectional.
- C: ✓ Correct. Masked positions get weight 0.
- D: ✗ Attending in both directions does not make weights symmetric. q_i·k_j ≠ q_j·k_i in general.

**Q151 → D**

Each head has an n × n weight matrix whose rows sum to 1. The output is a weighted average of value vectors, so its last dimension is d_v.

- A: ✗ QKᵀ contracts over d_k, leaving seq × seq.
- B: ✗ Heads stay separate until concatenation.
- C: ✗ Multiplying by V restores the last dimension to d_v = 64.
- D: ✓ Correct.

**Q152 → B**

band_part(…, −1, 0) keeps the lower triangle (row i has ones in columns 0…i). The whole sequence is still processed in parallel during training, while each position sees only its past.

- A: ✗ A padding mask depends on the input. This one is fixed and triangular.
- B: ✓ Correct. Masked scores become −1e9, which is zero after softmax.
- C: ✗ It is lower-triangular, so it blocks the future.
- D: ✗ Only the diagonal would be 1 in that case.

**Q153 → A**

Each (sin, cos) pair rotates as the position increases, so PE(pos + k) is a fixed linear map (a rotation) of PE(pos). pe is added to the token embeddings, not concatenated.

- A: ✓ Correct. Wavelengths range from 2π to 10000·2π.
- B: ✗ They are computed by formula. Nothing is learned.
- C: ✗ The frequency depends on i: low dimensions oscillate fast and high ones slowly.
- D: ✗ sin and cos stay in [−1, 1].

**Q154 → D**

Foster’s GPT example uses MultiHeadAttention(num_heads, key_dim) with key_dim per head. The output dense layer projects the concatenated heads back to the input width. It is a common exam trap to read key_dim as the total.

- A: ✗ In Keras, key_dim is the size per head.
- B: ✗ It is unrelated to sequence length.
- C: ✗ No.
- D: ✓ Correct. Parameters: 3·(256·512 + 512) + (512·256 + 256) = 526,080.

**Q155 → B**

Post-LN (shown here) applies the norm after the residual add. Pre-LN (GPT-2, ViT) normalizes the input to each sub-layer and tends to train more stably in deep stacks. Both use residual paths so gradients reach early layers.

- A: ✗ Normalization is applied after the add here, and + is a residual sum.
- B: ✓ Correct. This is the original Transformer layout.
- C: ✗ Positional encodings are added once, at the input.
- D: ✗ LayerNormalization normalizes per token, not across the batch.

**Q156 → C**

With sentence pairs it becomes [CLS] A [SEP] B [SEP], with token_type_ids 0 and 1, which is the BertViz setup from your homework.

- A: ✗ The tokenizer adds special tokens.
- B: ✗ Common words are whole tokens. ## marks a word-piece continuation for rarer words.
- C: ✓ Correct. BERT wraps every single sentence with [CLS] … [SEP].
- D: ✗ The uncased model lowercases its input.

**Q157 → B**

Each [layer][0, h] is a 15 × 15 row-stochastic matrix. BertViz’s model view draws this as a 12 × 12 grid of heads.

- A: ✗ There is one tensor per layer, with the heads stacked inside it.
- B: ✓ Correct.
- C: ✗ The head dimension is missing.
- D: ✗ It is a tuple with one tensor per layer.


---

## Class 5 · Autoregressive Models

**Q158.** ○ *Single answer.* How do autoregressive models differ from VAEs?

- ○ **A.** They are implicit models with no density, trained adversarially against a discriminator network
- ○ **B.** They factor p(x) as ∏ p(x_t | x_<t) and model the exact distribution, not a bound
- ○ **C.** They condition each prediction on a latent random variable
- ○ **D.** They generate the whole output in one parallel step

**Q159.** ☐ *Select all that apply.* Three ways of combining positional information with token embeddings were discussed. Which statements are correct? Select all that apply.

- ☐ **A.** Learned: trainable position embeddings, as in ViT
- ☐ **B.** The magnitude of the position vector does not matter, since attention normalizes everything
- ☐ **C.** Additive: the position vector is added element-wise; the dimension is unchanged
- ☐ **D.** Concatenation: position and token vectors are stacked, which increases the dimension

**Q160.** ☐ *Select all that apply.* In the RNN computational graph (Goodfellow et al.), which roles do U, W and V play? Select all that apply.

- ☐ **A.** V: hidden-to-output weights
- ☐ **B.** U, W and V are separate matrices at every time step, so the parameter count grows with sequence length
- ☐ **C.** U: input-to-hidden weights
- ☐ **D.** W: hidden-to-hidden recurrent weights

**Q161.** ☐ *Select all that apply.* Which statements about Backpropagation Through Time (BPTT) are correct? Select all that apply.

- ☐ **A.** BPTT avoids vanishing gradients because the gradients are summed across time steps rather than multiplied
- ☐ **B.** Because weights are shared, gradients from every time step are summed for each parameter
- ☐ **C.** The RNN is unrolled into a deep feedforward network with one layer per time step
- ☐ **D.** Loss can be computed at each step or only at the final step, depending on the task
- ☐ **E.** The gradient at time t includes terms from future time steps

**Q162.** ☐ *Select all that apply.* Which statements about LSTM gates are correct? Select all that apply.

- ☐ **A.** The forget gate sets the self-loop weight of the cell state through a sigmoid, between 0 and 1
- ☐ **B.** The output gate can shut off the cell’s output h_t
- ☐ **C.** All gates use ReLU activations, so that their outputs are unbounded and the gradients cannot saturate
- ☐ **D.** The input gate decides how much new information is written to the cell state

**Q163.** ○ *Single answer.* In a GRU, what happens when the reset gate is close to 0?

- ○ **A.** The GRU becomes an LSTM with three separate gates, gaining a dedicated output gate on the hidden state
- ○ **B.** The output h_t is forced to zero for that step, regardless of what the update gate says
- ○ **C.** The previous hidden state is copied unchanged to the next step
- ○ **D.** The candidate state ignores the previous hidden state and resets using only the current input

**Q164.** ○ *Single answer.* Luong et al. (2015) compared global and local attention for neural machine translation. Which statement is correct?

- ○ **A.** Attention reduced BLEU compared to non-attentional systems
- ○ **B.** Local attention predicts an aligned position p_t and attends to a small window around it
- ○ **C.** Global attention attends to a fixed-size window; local attention attends to all source words
- ○ **D.** Local attention always gives blurrier alignments than global attention, because a small window spreads weight more evenly

**Q165.** ☐ *Select all that apply.* PixelCNN uses masked convolutions. Which statements are correct? Select all that apply.

- ☐ **A.** Pixels are generated in raster-scan order, row by row and left to right
- ☐ **B.** The Type B mask, used in later layers, includes the center position
- ☐ **C.** Standard unmasked convolutions suffice because pixels already have a natural sequential ordering
- ☐ **D.** The Type A mask, used in the first layer, excludes the center pixel and all later pixels
- ☐ **E.** Masks are binary matrices multiplied element-wise with the filters

**Q166.** ○ *Single answer.* Why can a Type B mask include the center pixel without breaking the autoregressive property?

- ○ **A.** Because later layers are frozen during training and therefore cannot leak information about future pixels
- ○ **B.** It does break the property, but the error is small
- ○ **C.** After a Type A first layer, the center feature already depends only on earlier pixels
- ○ **D.** Because the center pixel is always zero after the first layer’s ReLU, so including it adds nothing

**Q167.** ○ *Single answer.* Using the sentence “I went to the bank to withdraw money,” what can a self-attention head linking “bank” and “withdraw” achieve?

- ○ **A.** It encodes the absolute position of “bank”
- ○ **B.** It predicts the next token after “money” by attending only to the final word
- ○ **C.** It disambiguates “bank” as a financial institution
- ○ **D.** It establishes subject–verb agreement between “I” and “went”

**Q168.** ○ *Single answer.* In an LSTM, which component carries information across long time spans through a linear self-loop?

- ○ **A.** The cell (state) unit s_t, whose self-loop weight is set by the forget gate
- ○ **B.** The output gate, which stores the previous output h_{t−1} and feeds it back unchanged
- ○ **C.** The softmax output layer, which keeps a running average of past predictions over time
- ○ **D.** The input feature unit, which uses a ReLU so that its activations never saturate across long time spans

**Q169.** ○ *Single answer.* Why is encoding an entire past sequence into one RNN hidden vector problematic?

- ○ **A.** The hidden vector cannot be updated after the first time step
- ○ **B.** A single vector is an inefficient bottleneck, and most of its context is irrelevant to the next step
- ○ **C.** The hidden vector grows linearly with the sequence length, which quickly exhausts the available GPU memory
- ○ **D.** RNNs cannot process text

**Q170.** ○ *Single answer.* A sequence-to-sequence RNN with attention translates “A B C D” into “X Y Z <eos>”. What does the <eos> token do?

- ○ **A.** It indicates an unknown word that was not in the vocabulary when the model was trained
- ○ **B.** It marks the end of the sentence so the decoder knows when to stop
- ○ **C.** It is the attention context vector
- ○ **D.** It encodes the absolute position of the last source word so that local attention can center its window

**Q171.** ○ *Single answer.* PixelCNN outputs, for each pixel, what kind of prediction?

- ○ **A.** A probability distribution over the pixel’s values given earlier pixels
- ○ **B.** A noise estimate as in diffusion
- ○ **C.** A single deterministic pixel value with no uncertainty
- ○ **D.** A latent vector for a VAE decoder, which then reconstructs the full image in one forward pass

**Q172.** ○ *Single answer.* A GRU’s update gate u_t close to 1 (in the Goodfellow formulation) means

- ○ **A.** the previous hidden state is mostly copied forward
- ○ **B.** the reset gate is disabled and the GRU behaves like a plain feed-forward layer for that step
- ○ **C.** the state is fully replaced by the new candidate
- ○ **D.** the output is zero

**Q173.** ☐ *Select all that apply.* Which are typical applications of LSTMs? Select all that apply.

- ☐ **A.** Time-series forecasting
- ☐ **B.** Audio classification
- ☐ **C.** Sentiment analysis
- ☐ **D.** Computing exact image likelihoods by modeling pixels with masked convolutions in raster order
- ☐ **E.** Text generation

**Q174.** ○ *Single answer.* In ViT, how are learned positional embeddings handled?

- ○ **A.** They are computed from pixel coordinates by a CNN
- ○ **B.** They are fixed sinusoids
- ○ **C.** They are concatenated to each patch embedding, which doubles the model width for every layer
- ○ **D.** They are trainable vectors, the same size as the patch embeddings, added to them

**Q175.** ○ *Single answer.* A student builds a PixelCNN and uses a Type A mask in every layer, not just the first. What is the most likely consequence?

- ○ **A.** Still valid, but it wastes context: each layer drops info from the pixel directly to the left
- ○ **B.** The softmax over the 256 pixel values can no longer be normalized, because masked weights are exactly zero
- ○ **C.** The model can see the pixel it predicts and learns to copy it
- ○ **D.** The model generates pixels column by column

**Q176.** ○ *Single answer.* An LSTM’s forget-gate bias is initialized to a large negative value (e.g., −5). What is the most likely effect early in training?

- ○ **A.** The cell keeps information for a very long time
- ○ **B.** The cell wipes its state each step, so the LSTM behaves like a short-memory RNN
- ○ **C.** The output gate takes over the forgetting role automatically, because the gates share their parameters
- ○ **D.** Training diverges because gradients explode

**Q177.** ○ *Single answer.* To save memory, a student uses truncated BPTT with a window of 20 steps on sequences of length 500. What is the main limitation?

- ○ **A.** Gradients flow back at most 20 steps, so longer dependencies cannot be learned directly
- ○ **B.** The forward pass can no longer process sequences longer than 20
- ○ **C.** Parameter sharing is lost, because each 20-step window learns its own separate copy of the weights
- ○ **D.** The loss can only be computed at the last step

**Q178.** ○ *Single answer.* In a GRU (Goodfellow convention, h_t = u ⊙ h_{t−1} + (1 − u) ⊙ h̃), the update gate saturates at u ≈ 1 for all units. What happens?

- ○ **A.** The state is replaced by the new candidate at every step
- ○ **B.** The state is frozen: inputs barely affect it, but gradients pass back easily
- ○ **C.** The GRU becomes identical to an LSTM
- ○ **D.** The reset gate takes over and copies the input directly into the hidden state without any nonlinearity

**Q179.** ○ *Single answer.* An RNN language model is trained with BPTT, and the gradient norm suddenly spikes to 1e6 on a few batches. Which fix targets this directly?

- ○ **A.** Use a Type A mask
- ○ **B.** Remove the tanh nonlinearity so that the hidden state is a purely linear function of the inputs over time
- ○ **C.** Increase the learning rate
- ○ **D.** Gradient clipping: rescale the gradient when its norm exceeds a threshold

**Q180.** ○ *Single answer.* Input shape is (batch, 20, 100). What are the output shape and parameter count of each LSTM?

```python
A = layers.LSTM(128, return_sequences=True)(x)
B = layers.LSTM(128)(x)
```

- ○ **A.** Both (batch, 20, 128), because return_sequences only changes what is returned during training, not inference
- ○ **B.** A: (batch, 20, 128); B: (batch, 128); 117,248 parameters each
- ○ **C.** A: (batch, 20, 100); B: (batch, 100)
- ○ **D.** A: (batch, 128); B: (batch, 20, 128); 51,712 parameters each

**Q181.** ○ *Single answer.* What does this optimizer setting address in RNN training?

```python
optimizer = tf.keras.optimizers.Adam(learning_rate=1e-3, clipnorm=1.0)
model.compile(optimizer=optimizer, loss="sparse_categorical_crossentropy")
```

- ○ **A.** Overfitting, by adding weight decay to the recurrent kernel so that the weights stay small
- ○ **B.** Exploding gradients: gradient norms above 1.0 are rescaled to 1.0
- ○ **C.** Slow convergence, by doubling the learning rate whenever the loss plateaus
- ○ **D.** Vanishing gradients

**Q182.** ○ *Single answer.* Given the next-token probabilities [0.5, 0.3, 0.2], what does sample_with_temperature compute at temperature 0.5?

```python
def sample_with_temperature(probs, temperature):
    probs = probs ** (1 / temperature)
    probs = probs / np.sum(probs)
    return np.random.choice(len(probs), p=probs)
```

- ○ **A.** ≈[0.658, 0.237, 0.105]: sharper, favoring the top token
- ○ **B.** [0.5, 0.3, 0.2], unchanged
- ○ **C.** ≈[0.415, 0.322, 0.263], flatter, because a lower temperature always spreads probability more evenly
- ○ **D.** [1, 0, 0]

**Q183.** ☐ *Select all that apply.* In this PixelCNN masked-convolution layer (kernel_size = 3), which statements are correct? Select all that apply.

```python
def build(self, input_shape):
    self.conv.build(input_shape)
    kernel_shape = self.conv.kernel.get_shape()
    self.mask = np.zeros(shape=kernel_shape)
    self.mask[: kernel_shape[0] // 2, ...] = 1.0
    self.mask[kernel_shape[0] // 2, : kernel_shape[1] // 2, ...] = 1.0
    if self.mask_type == "B":
        self.mask[kernel_shape[0] // 2, kernel_shape[1] // 2, ...] = 1.0

def call(self, inputs):
    self.conv.kernel.assign(self.conv.kernel * self.mask)
    return self.conv(inputs)
```

- ☐ **A.** For mask_type 'A', the center and everything to its right in the middle row stay 0
- ☐ **B.** For mask_type 'B', the center weight is also set to 1
- ☐ **C.** All rows below the center are zeroed for both types
- ☐ **D.** The mask is applied once at initialization, so the masked weights can grow back during training

**Q184.** ○ *Single answer.* How many forward passes does this PixelCNN generation loop make for one 32×32 image, and why can it not be parallelized?

```python
generated = np.zeros((1, 32, 32, 1))
for row in range(32):
    for col in range(32):
        probs = model.predict(generated, verbose=0)[:, row, col, :]
        generated[:, row, col, 0] = sample_with_temperature(probs[0], 1.0) / 255.0
```

- ○ **A.** 1, because the network sees the whole image at once
- ○ **B.** 10, one per epoch
- ○ **C.** 1,024: each pixel depends on the ones just sampled
- ○ **D.** 32, one per row, because all pixels in a row are predicted together from the rows above them


### Answer key — Class 5 · Autoregressive Models

**Q158 → B**

Autoregressive models turn generation into a sequential process conditioned on previous values (word by word or pixel by pixel), with explicit modeling of the data-generating distribution. VAEs instead optimize the ELBO approximation.

- A: ✗ That describes GANs.
- B: ✓ Correct. Autoregressive models belong to the tractable explicit-density family.
- C: ✗ That describes VAEs.
- D: ✗ Generation is sequential, one token or pixel at a time.

**Q159 → A, C, D**

Design criteria: positions must be distinct; magnitudes must be controlled; and the method should balance mixing information against computational complexity. Example: “Engineer” −0.9748 + position 0.1566 = −0.8182 under the additive scheme.

- A: ✓ Correct.
- B: ✗ If ‖position vector‖ ≫ ‖token vector‖, the sum is dominated by position, and two different words at the same position look alike to QKᵀ.
- C: ✓ Correct.
- D: ✓ Correct.

**Q160 → A, C, D**

h_t = tanh(b + W h_{t−1} + U x_t), o_t = c + V h_t, ŷ_t = softmax(o_t). The loss compares ŷ_t to the target y_t at each step.

- A: ✓ Correct.
- B: ✗ Parameters are shared across time steps, which is why BPTT sums their gradients.
- C: ✓ Correct.
- D: ✓ Correct.

**Q161 → B, C, D, E**

Long sequences (over 1,000 tokens) need about 1,000 matrix products forward and another 1,000 backward, which brings memory pressure and numerical instability. These are the motivations for LSTMs and attention.

- A: ✗ Summation is across occurrences of a parameter, but each term still contains a product of many Jacobians, so gradients still vanish or explode.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✓ Correct, because h_t affects all later hidden states and losses.

**Q162 → A, B, D**

The linear self-loop of the cell state, gated by the forget gate, lets gradients flow over hundreds of steps, which addresses the vanishing gradient problem (Hochreiter & Schmidhuber, 1997). Applications: time-series forecasting, sentiment analysis, audio classification, text generation.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✗ Gates use sigmoids so their values lie in (0, 1). The input unit can use any squashing nonlinearity, e.g., tanh.
- D: ✓ Correct.

**Q163 → D**

A GRU has two gates. The update gate u controls how much of the previous state carries over (it plays the roles of forget and input gate together). The reset gate r controls which parts of the past state feed into the candidate state, which lets the GRU drop information that turns out to be irrelevant.

- A: ✗ No such conversion happens.
- B: ✗ The reset gate does not zero the output.
- C: ✗ Copying is controlled by the update gate.
- D: ✓ Correct.

**Q164 → B**

Global: a variable-length alignment vector over all source states, with dot-product scoring working best. Local: monotonic or predictive variants, with the general scoring function best for predictive alignment; the context vector comes only from the window.

- A: ✗ Attention gave about +5.0 BLEU, and an ensemble reached 25.9 BLEU on WMT’15 English→German.
- B: ✓ Correct.
- C: ✗ This is reversed.
- D: ✗ Local attention gives sharper alignments with limited context; global attention tends to be blurrier.

**Q165 → A, B, D, E**

PixelCNN is trained autoregressively, using masked conv layers to enforce ordering and residual blocks (skip connections) for depth. Each pixel is conditioned only on previously generated pixels.

- A: ✓ Correct.
- B: ✓ Correct. After the first layer, the center feature already encodes only past pixels.
- C: ✗ Standard convolutions see future pixels. Masking imposes the ordering.
- D: ✓ Correct. The prediction cannot depend on the pixel’s own value.
- E: ✓ Correct.

**Q166 → C**

Information about pixel i itself enters only through the input. The Type A mask blocks it at the first layer, and every later feature at position i aggregates only from predecessors, so Type B layers can safely use the center.

- A: ✗ Later layers are trained.
- B: ✗ It does not break the property.
- C: ✓ Correct.
- D: ✗ Pixels are not zero in general.

**Q167 → C**

The mechanism: the query for “bank” scores high against the key for “withdraw”, so the value of “withdraw” is mixed into bank’s new representation, moving it toward the finance sense. Other heads can capture other relations, e.g., head 1 links I–went (actor); head 2 went–to the bank (destination); head 3 bank–withdraw (purpose); head 4 withdraw–money (action–object); head 5 bank–withdraw for contextual meaning. Different heads capture different relations at the same time.

- A: ✗ Positional encodings do that.
- B: ✗ That is not described.
- C: ✓ Correct.
- D: ✗ That is a different head’s pattern.

**Q168 → A**

s_t = f_t ⊙ s_{t−1} + g_t ⊙ (input feature). Because this update is additive, with a gate-controlled linear self-loop, gradients can flow across many steps when f_t ≈ 1. The gating units can also take s_{t−1} as an extra input (peephole connections).

- A: ✓ Correct.
- B: ✗ The output gate only controls how much of the cell is exposed as h_t.
- C: ✗ Not part of the recurrence.
- D: ✗ The input unit computes candidate content. It does not carry memory across time.

**Q169 → B**

A fixed-size vector has fixed capacity, so as the sequence grows, old information must be overwritten. Gradients to early steps also vanish (see the BPTT code). Attention keeps every past state and retrieves only the relevant ones on demand.

- A: ✗ It is updated at every step.
- B: ✓ Correct.
- C: ✗ The hidden vector has a fixed size. That fixed size is the problem.
- D: ✗ They can. LSTMs are used for text generation and sentiment analysis.

**Q170 → B**

Autoregressive decoders generate until they emit <eos>. This lets them produce variable-length outputs, as in Luong et al.’s stacked recurrent NMT architecture.

- A: ✗ That is usually <unk>.
- B: ✓ Correct.
- C: ✗ The context vector is computed from source states, not a token.
- D: ✗ It is a vocabulary symbol, not a positional encoding.

**Q171 → A**

Generation samples one pixel at a time from p(x_i | x_<i) in raster order, feeding each new pixel back in. This is slow but gives an exact likelihood.

- A: ✓ Correct.
- B: ✗ That is diffusion.
- C: ✗ Autoregressive models output distributions to sample from.
- D: ✗ PixelCNN has no latent variable.

**Q172 → A**

h_t = u ⊙ h_{t−1} + (1 − u) ⊙ candidate. Update gates can copy dimensions or replace them with the target state at the sigmoid extremes. Conventions differ between sources, so check which one the exam uses.

- A: ✓ Correct.
- B: ✗ The two gates act independently.
- C: ✗ In Goodfellow’s notation, u near 1 keeps the old state.
- D: ✗ Not what the gate does.

**Q173 → A, B, C, E**

Advantages: learning long-term dependencies, robustness to vanishing gradients, a flexible architecture, and wide framework support (Keras LSTM and GRU layers).

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✗ That describes PixelCNN.
- E: ✓ Correct.

**Q174 → D**

Class 5 uses ViT as the example of learned positional embeddings: initialized as parameters and optimized with the rest of the model.

- A: ✗ No CNN is involved.
- B: ✗ ViT learns them.
- C: ✗ They are added, not concatenated.
- D: ✓ Correct.

**Q175 → A**

After layer 1, the center feature at position i depends only on pixels before i, so it is safe to read. Mask A in later layers blocks that safe information. Each extra Type A layer removes the immediate predecessor from what the next layer can use, so dependencies that should take one hop are lost. The code panel prints both masks.

- A: ✓ Correct. The order stays valid, but the receptive field gains a blind region and the model weakens.
- B: ✗ Masking the filters does not affect the output softmax.
- C: ✗ Type A masks hide the center, so nothing can be copied. That failure comes from Type B in the first layer.
- D: ✗ The mask shape defines raster order. Using Type A everywhere does not change the order.

**Q176 → B**

c_t = f ⊙ c_{t−1} + i ⊙ g. With f ≈ 0, c_t ≈ i ⊙ g, so nothing carries over. This is why practitioners usually initialize the forget bias positive (e.g., +1), the opposite of this scenario. The LSTM code panel uses a +6 bias to show the cell state persisting across 100 steps.

- A: ✗ A sigmoid of −5 is about 0.007. The gate is nearly closed, which means forgetting.
- B: ✓ Correct. Gradients through the cell path are multiplied by f ≈ 0.
- C: ✗ Each gate has its own parameters.
- D: ✗ A near-zero multiplier makes gradients vanish, not explode.

**Q177 → A**

Truncation cuts the backward graph. The state h is passed forward but treated as a constant at the window boundary, so ∂L/∂(earlier steps) is never computed. This saves memory and avoids the long Jacobian products, at the cost of a dependency horizon of about 20.

- A: ✓ Correct.
- B: ✗ The hidden state can still be carried forward across windows.
- C: ✗ The weights are still shared everywhere.
- D: ✗ The loss is still computed at every step.

**Q178 → B**

This is the GRU version of an LSTM with forget ≈ 1 and input ≈ 0: perfect memory, no new information. Learning lives between these extremes. The GRU code panel shows u = 0.999 returning h_prev unchanged.

- A: ✗ That would be u ≈ 0.
- B: ✓ Correct. ∂h_t/∂h_{t−1} ≈ I.
- C: ✗ No.
- D: ✗ The reset gate only shapes the candidate h̃.

**Q179 → D**

Exploding gradients come from products of Jacobians with norm above 1. They are rare but catastrophic. Clipping keeps the direction and bounds the magnitude. Vanishing gradients need architectural fixes instead (LSTM, GRU, attention, residual connections).

- A: ✗ That is a PixelCNN concept.
- B: ✗ A linear RNN explodes or vanishes even more readily, through powers of W.
- C: ✗ That would amplify the explosion.
- D: ✓ Correct. It caps the size of the step.

**Q180 → B**

An LSTM has 4 blocks (input, forget and output gates, plus the candidate), each with input weights, recurrent weights and a bias. Stacking LSTMs needs return_sequences=True on every layer except the last.

- A: ✗ Without return_sequences, only the last time step’s output is returned.
- B: ✓ Correct. 4·(128·(100 + 128) + 128) = 117,248.
- C: ✗ The units (128) set the output width, not the input width.
- D: ✗ The outputs are swapped, and an LSTM has 4 gate blocks.

**Q181 → B**

BPTT multiplies many Jacobians, so occasional gradient spikes can wreck training. clipnorm keeps the gradient direction but bounds its length. Vanishing gradients instead need gating (LSTM, GRU), attention or skip connections.

- A: ✗ clipnorm is not weight decay.
- B: ✓ Correct.
- C: ✗ No.
- D: ✗ Clipping caps large gradients. It cannot enlarge small ones.

**Q182 → A**

Temperature controls diversity in autoregressive generation, for text with LSTMs or GPT. A low T is safe and repetitive; a high T is creative and error-prone.

- A: ✓ Correct. p^(1/T) renormalized, which squares and renormalizes at T = 0.5.
- B: ✗ That is temperature 1.0.
- C: ✗ That is T = 2.0. Lower T sharpens the distribution.
- D: ✗ That is the limit T → 0 (greedy argmax).

**Q183 → A, B, C**

The resulting 3×3 Type A mask is [[1, 1, 1], [1, 0, 0], [0, 0, 0]] and Type B is [[1, 1, 1], [1, 1, 0], [0, 0, 0]]. Multiplying the kernel by the mask on every call enforces the autoregressive ordering.

- A: ✓ Correct. Only rows above and pixels to the left are set to 1.
- B: ✓ Correct. That is the only difference from Type A.
- C: ✓ Correct. Pixels below come later in raster order.
- D: ✗ The mask multiplies the kernel at every forward pass, so masked weights never take effect.

**Q184 → C**

Training is parallel thanks to masking: all targets are known. Generation is sequential, since pixel (r, c) needs the sampled values before it. This is the main cost of autoregressive models, the same as token-by-token GPT decoding.

- A: ✗ Each pixel must be sampled before the next one can be predicted.
- B: ✗ No.
- C: ✓ Correct. Sampling is sequential, even though training was parallel.
- D: ✗ Masks condition each pixel on the pixels to its left in the same row too.


---

## Class 6 · Multimodal LLMs

**Q185.** ○ *Single answer.* How does Byte Pair Encoding (BPE) build its vocabulary?

- ○ **A.** It clusters words by embedding similarity using k-means, then assigns each cluster a single shared token id
- ○ **B.** It splits text into fixed 4-character chunks and assigns each distinct chunk its own token id
- ○ **C.** It starts from single characters and repeatedly merges the most frequent adjacent pair
- ○ **D.** It assigns one token to each whole word in the training corpus

**Q186.** ☐ *Select all that apply.* Which statements about GPT-2’s adaptive input representations and adaptive softmax are correct? Select all that apply.

- ☐ **A.** Adaptive softmax clusters the vocabulary by frequency to cut the cost of the output layer
- ☐ **B.** In the 10,000-word example, the 100 most frequent words form the first cluster and are updated most often
- ☐ **C.** Adaptive softmax computes the exact full softmax over the vocabulary, only reordering words so the frequent ones are cached
- ☐ **D.** Adaptive input gives frequent words larger embeddings and rare words smaller ones

**Q187.** ☐ *Select all that apply.* Which statements about the Vision Transformer (ViT) are correct? Select all that apply.

- ☐ **A.** Images are split into fixed patches (e.g., 16×16) and linearly projected
- ☐ **B.** Layer norm comes before each block, residuals after, and the MLP has two layers with GELU
- ☐ **C.** ViT keeps CNN inductive biases such as locality and translation equivariance in every layer
- ☐ **D.** A learnable [class] token is prepended, and learnable 1-D position embeddings are added

**Q188.** ○ *Single answer.* ViT experiments compared 1-D, 2-D and relative positional embeddings. What did they find?

- ○ **A.** All three performed similarly; learned 1-D embeddings still captured 2-D structure
- ○ **B.** 2-D embeddings were essential; 1-D embeddings failed to learn any spatial structure
- ○ **C.** Relative embeddings dramatically outperformed the alternatives by more than ten points of ImageNet accuracy
- ○ **D.** Removing positional embeddings had no effect at all

**Q189.** ○ *Single answer.* Mean attention distance in ViT, measured across layers, shows which pattern?

- ○ **A.** Early layers mix local and global heads; late layers are mostly global
- ○ **B.** Distance decreases with depth, so the final layers attend only to each patch’s immediate neighbors
- ○ **C.** All heads in all layers attend only to neighboring patches
- ○ **D.** Distance is constant across layers

**Q190.** ○ *Single answer.* “QFormer” in the vision-transformer lecture (Zhang et al., 2024) refers to quadrangle attention. What does it change?

- ○ **A.** It removes self-attention entirely and uses learned geometric transforms of the image instead
- ○ **B.** It replaces patches with individual pixels so that attention windows can take any shape
- ○ **C.** It is the same module as BLIP-2’s Querying Transformer that bridges a frozen image encoder and a frozen LLM
- ○ **D.** It learns a transform that deforms fixed square windows into quadrangles fitting objects

**Q191.** ☐ *Select all that apply.* Which statements about CLIP’s training are correct? Select all that apply.

- ☐ **A.** It jointly trains an image encoder and a text encoder to predict which image and text belong together in a batch
- ☐ **B.** It uses a symmetric cross-entropy loss over cosine similarities between image and text embeddings
- ☐ **C.** It is trained to generate captions autoregressively, since generation is more compute-efficient than contrastive learning
- ☐ **D.** Its pretraining set, WIT, has about 400 million image–text pairs gathered with 500,000 queries

**Q192.** ○ *Single answer.* How does CLIP perform zero-shot classification on a new dataset?

- ○ **A.** It fine-tunes a linear head on a few labeled examples from the new dataset
- ○ **B.** It uses k-means clustering on the image embeddings
- ○ **C.** It embeds class names or descriptions with the text encoder and picks the class most similar to the image
- ○ **D.** It retrains the image encoder on the new classes, freezing the text encoder so that the label space stays fixed

**Q193.** ☐ *Select all that apply.* Which are known limitations and risks of CLIP? Select all that apply.

- ☐ **A.** It cannot recognize text in images at all, failing even on MNIST digits and rendered sentiment text
- ☐ **B.** It struggles with specialized tasks such as lymph-node tumor detection (PatchCamelyon)
- ☐ **C.** Web-scraped training data can contain and amplify social biases
- ☐ **D.** Flexible zero-shot classifiers could be misused, e.g., for unauthorized surveillance

**Q194.** ○ *Single answer.* DALL·E 2 consists of three parts. What is the role of the prior?

- ○ **A.** It converts the text prompt into a CLIP text embedding
- ○ **B.** It generates the final pixels, conditioned on both the text prompt and the predicted image embedding
- ○ **C.** It maps the CLIP text embedding to a predicted CLIP image embedding
- ○ **D.** It filters unsafe prompts and rewrites them before they reach the text encoder and decoder

**Q195.** ☐ *Select all that apply.* Which statements about BLIP and BLIP-2 are correct? Select all that apply.

- ☐ **A.** CapFilt generates synthetic captions and filters noisy web captions
- ☐ **B.** BLIP-2 keeps the image encoder and the LLM frozen and trains a Q-Former between them
- ☐ **C.** BLIP introduces a Multimodal mixture of Encoder–Decoder (MED) for understanding and generation tasks
- ☐ **D.** In BLIP-2, Q-Former outputs are projected and fed to the LLM as a soft visual prompt
- ☐ **E.** BLIP-2 fine-tunes every weight of the vision transformer and the LLM end-to-end, since frozen components would block gradients

**Q196.** ○ *Single answer.* Pic2Word addresses zero-shot composed image retrieval (CIR). How is its mapping network trained?

- ○ **A.** On unlabeled images, mapping each frozen CLIP image embedding to a pseudo-word token
- ○ **B.** On labeled triplets of (reference image, modification text, target image)
- ○ **C.** By fine-tuning the whole CLIP model end-to-end on a large collection of sketches, cartoons and other domains
- ○ **D.** With a GAN discriminator that judges whether the composed query looks like a real caption

**Q197.** ☐ *Select all that apply.* Which statements about ScreenAI are correct? Select all that apply.

- ☐ **A.** It reaches state of the art on UI and infographic tasks with only 5B parameters
- ☐ **B.** It combines the PaLI architecture with Pix2Struct’s flexible patching
- ☐ **C.** It is a decoder-only model that skips the vision encoder and reads raw HTML source instead of screenshots
- ☐ **D.** A textual screen schema from automatic annotation, plus LLM-generated tasks, provides pretraining data

**Q198.** ☐ *Select all that apply.* Which statements about Flamingo’s architecture are correct? Select all that apply.

- ☐ **A.** A frozen NFNet-F6 vision encoder, pretrained with a CLIP-style contrastive loss, extracts features
- ☐ **B.** The Perceiver Resampler maps variable-size visual features to a fixed set of 64 visual tokens
- ☐ **C.** Frozen LM blocks are interleaved with new GATED XATTN-DENSE cross-attention blocks
- ☐ **D.** The gates use tanh(α) with α initialized to 0, so the model starts identical to the original LM
- ☐ **E.** The language model is fully fine-tuned from scratch on interleaved image–text data so it can learn visual grounding

**Q199.** ○ *Single answer.* Why are Flamingo’s cross-attention outputs multiplied by tanh(α) with α initialized to 0?

- ○ **A.** To enforce sparsity in the attention weights, so each token attends to at most one visual token
- ○ **B.** Because tanh is required for the softmax to be stable
- ○ **C.** So the model starts out exactly like the frozen LM, for stable training
- ○ **D.** To speed up inference by skipping the vision encoder at test time

**Q200.** ☐ *Select all that apply.* Which are known limitations of Flamingo? Select all that apply.

- ☐ **A.** In-context learning is sensitive to demonstration quality and scales poorly beyond the low-data regime
- ☐ **B.** It inherits weaknesses of the pretrained LM, such as hallucinations and ungrounded guesses
- ☐ **C.** It cannot process video at all, because the Perceiver Resampler only accepts a single still image per sequence
- ☐ **D.** Its classification performance trails contrastive models optimized for image–text retrieval

**Q201.** ○ *Single answer.* A multimodal embedding model such as CLIP is valuable mainly because it

- ○ **A.** generates high-resolution images directly from text without any decoder or prior network
- ○ **B.** requires no training data, because the embeddings come from a fixed, hand-designed feature extractor
- ○ **C.** puts several modalities in one shared, directly comparable vector space
- ○ **D.** stores images and text in separate, incompatible vector spaces

**Q202.** ○ *Single answer.* Why does the Perceiver Resampler help Flamingo?

- ○ **A.** It fine-tunes the vision encoder, which would otherwise stay random because it is never pretrained
- ○ **B.** It replaces the language model
- ○ **C.** It increases the number of visual tokens for higher fidelity
- ○ **D.** It turns any number of visual features into 64 tokens, cutting cross-attention cost

**Q203.** ○ *Single answer.* How does Flamingo’s vision encoder differ from a CLIP ViT image encoder?

- ○ **A.** They are identical
- ○ **B.** Flamingo trains its encoder from scratch with a captioning loss, as part of the full model
- ○ **C.** Flamingo uses a ViT, while CLIP uses no image encoder
- ○ **D.** Flamingo uses a frozen NFNet-F6, trained with a CLIP-style contrastive loss

**Q204.** ☐ *Select all that apply.* Which tasks does composed image retrieval (CIR) cover in Pic2Word? Select all that apply.

- ☐ **A.** Object composition, e.g., adding or removing objects
- ☐ **B.** Attribute editing, e.g., changing color or texture
- ☐ **C.** Generating new pixels for the modified image with a diffusion decoder conditioned on the pseudo token
- ☐ **D.** Domain conversion, e.g., real photo to sketch or cartoon

**Q205.** ○ *Single answer.* Reported zero-shot CLIP robustness: by how much did it reduce the accuracy gap between ImageNet and natural-distribution-shift datasets?

- ○ **A.** By up to 75%
- ○ **B.** It widened the gap
- ○ **C.** By up to 10%
- ○ **D.** It closed the gap completely on all seven shift datasets, so it reached 100% of ImageNet accuracy

**Q206.** ○ *Single answer.* Compute for AI models other than Transformers grew by about 2× every 8 months. What is the takeaway for LLM training?

- ○ **A.** Any university lab can train GPT-3-scale models on a single GPU in a few days with standard tools
- ○ **B.** Data is no longer a constraint
- ○ **C.** Cost, data and expertise rise steeply; one GPT-3 run can cost over $12M
- ○ **D.** Compute requirements are shrinking

**Q207.** ○ *Single answer.* What does probs[0] represent?

```python
texts = ["a photo of a cat", "a photo of a dog", "a photo of a car"]
inputs = processor(text=texts, images=[img1, img2], return_tensors="pt", padding=True)
outputs = model(**inputs)
probs = outputs.logits_per_image.softmax(dim=1)     # shape (2, 3)
```

- ○ **A.** Probabilities over the 2 images for text 0
- ○ **B.** Pixel-wise segmentation probabilities for image 0, one value per image patch
- ○ **C.** A distribution over the 3 captions for image 0: zero-shot classification
- ○ **D.** The CLIP training loss

**Q208.** ○ *Single answer.* Why does the CLIP loss average two cross-entropies, one on logits and one on logits.T?

```python
logits = (image_emb @ text_emb.T) * logit_scale.exp()
labels = torch.arange(N)
loss = (F.cross_entropy(logits, labels) + F.cross_entropy(logits.T, labels)) / 2
```

- ○ **A.** To double the batch size
- ○ **B.** Symmetry: rows match images to texts, columns texts to images
- ○ **C.** Because cross-entropy only accepts square matrices, so the transpose fixes the shape mismatch between modalities
- ○ **D.** To regularize the temperature

**Q209.** ○ *Single answer.* A 224×224×3 batch is patchified as follows. What is the shape of patches, and the ViT sequence length after adding [class]?

```python
patches = tf.image.extract_patches(images, sizes=[1,16,16,1], strides=[1,16,16,1],
                                   rates=[1,1,1,1], padding="VALID")
```

- ○ **A.** (B, 7, 7, 3,072); 50
- ○ **B.** (B, 16, 16, 588); 257
- ○ **C.** (B, 14, 14, 768); 197
- ○ **D.** (B, 224, 224, 3); 50,176, since extract_patches returns one token per pixel

**Q210.** ○ *Single answer.* What is the output of this gated cross-attention block at initialization?

```python
self.alpha = tf.Variable(0.0)          # learnable, initialized at 0
def call(self, y, visual_tokens):
    return y + tf.tanh(self.alpha) * self.xattn(y, visual_tokens)
```

- ○ **A.** Zero, because the gate removes the language-model stream entirely at the beginning of training
- ○ **B.** Random, because the new layers are randomly initialized
- ○ **C.** Exactly y: the frozen LM is unchanged at the start
- ○ **D.** y multiplied by 0.5


### Answer key — Class 6 · Multimodal LLMs

**Q185 → C**

Example: if “t”+“h” is the most frequent pair, it becomes the single symbol “th”. The process repeats thousands of times over the corpus. The final vocabulary ranges from single characters to multi-character sequences, so any string can be encoded.

- A: ✗ BPE is frequency-based merging, not clustering.
- B: ✗ Merges are data-driven, not fixed-length.
- C: ✓ Correct. Subwords like “pre” and “ing” emerge.
- D: ✗ Word-level vocabularies cannot handle unseen words. BPE builds subwords.

**Q186 → A, B, D**

Both techniques spend capacity and compute on the words that matter most, with minimal performance loss (Joulin et al., 2017). GPT-3 (175B parameters, June 2020) added sparse attention, multi-head refinements and pipeline optimizations.

- A: ✓ Correct.
- B: ✓ Correct. The next 900 form cluster 2 and the remaining 9,000 rare words form cluster 3.
- C: ✗ It is an approximation. Rare words are handled through a cluster representation at level 1.
- D: ✓ Correct.

**Q187 → A, B, D**

Hybrid alternatives apply self-attention to CNN feature maps or use local self-attention. A full Transformer over high-resolution pixels is computationally expensive, which is why ViT works on patches.

- A: ✓ Correct. Hence “An Image is Worth 16×16 Words.”
- B: ✓ Correct.
- C: ✗ ViT lacks these biases, which is a key challenge and why it needs large-scale data.
- D: ✓ Correct.

**Q188 → A**

Visualizations show 1-D embeddings assigning similar vectors to patches in the same row or column. 1-D embeddings are also the most computationally efficient, which is why they are the default.

- A: ✓ Correct.
- B: ✗ 1-D embeddings learned 2-D structure on their own.
- C: ✗ Differences were minimal.
- D: ✗ The comparison was among embedding types. Some positional information still matters.

**Q189 → A**

Mean attention distance is the average image-space distance between a query patch and the patches it attends to, weighted by attention. It is loosely analogous to the receptive field size in CNNs. Global integration in late layers supports the final prediction, and attention maps highlight semantically relevant regions.

- A: ✓ Correct.
- B: ✗ This is reversed.
- C: ✗ Some heads attend globally even in early layers.
- D: ✗ It changes systematically with depth.

**Q190 → D**

The transformation matrix is decomposed into scaling, shearing, rotation, translation and projection, which makes optimization easier. Benefits: adaptive regions, cross-window information exchange, and computational cost comparable to fixed-window ViTs. The hierarchical variant merges tokens at each stage while increasing channels.

- A: ✗ It modifies window attention. It does not remove attention.
- B: ✗ Patch tokenization is kept.
- C: ✗ This is a naming trap. BLIP-2’s Q-Former is a different model.
- D: ✓ Correct.

**Q191 → A, B, D**

Steps: embed images and texts, compute cosine similarity, then update both encoders so matching pairs score high and mismatched pairs low. CLIP was trained with ResNet and ViT image encoders and a Transformer text encoder. The code below computes the symmetric loss and a zero-shot prediction.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✗ The contrastive objective was chosen because it is more efficient than generative or autoregressive prediction.
- D: ✓ Correct. There are up to 20,000 pairs per query for balance.

**Q192 → C**

Zero-shot CLIP is competitive with a fully supervised ResNet-50 linear probe across many datasets and matches 4-shot logistic regression. It is more robust to natural distribution shift, closing the ImageNet-to-shift-set gap by up to 75%. Fine-tuning on ImageNet reduces this robustness.

- A: ✗ That is few-shot linear probing, not zero-shot.
- B: ✗ Not how CLIP classifies.
- C: ✓ Correct.
- D: ✗ No training is involved in zero-shot transfer.

**Q193 → B, C, D**

Emergent capabilities from natural-language supervision include OCR, facial emotion recognition (comparable to humans on FER2013), action recognition (UCF101, Kinetics-700) and geolocalization. Future directions include larger and better data, better benchmarks, and responsible deployment.

- A: ✗ OCR is one of CLIP’s emergent capabilities (MNIST, SST2).
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.

**Q194 → C**

Pipeline: text encoder → prior → decoder. One version of the prior is an autoregressive encoder–decoder Transformer trained on CLIP text–image pairs to reproduce the CLIP image embedding from the CLIP text embedding. The paper also explores a diffusion prior. Providing the image embedding gives the decoder extra context and more accurate generations.

- A: ✗ That is the text encoder (a frozen CLIP model).
- B: ✗ That is the decoder.
- C: ✓ Correct.
- D: ✗ Not its role.

**Q195 → A, B, C, D**

BLIP-2 stage 1: representation learning, training the Q-Former on frozen ViT outputs plus captions with three contrastive-like objectives. Stage 2: generative learning, connecting to the frozen LLM through a projection layer. Earlier models handled either understanding (retrieval) or generation (captioning); BLIP unifies both.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✗ Keeping both frozen is the point. Only the Q-Former and projection are trained.

**Q196 → A**

The mapping network f_M is trained with a contrastive loss so that the text embedding of the pseudo token s* reconstructs the image embedding. At inference: encode the query image, map it to s*, insert it into a prompt such as “a sketch of *”, and retrieve by cosine similarity. Applications include attribute editing, object composition and domain conversion.

- A: ✓ Correct.
- B: ✗ Pic2Word avoids costly triplets. That is what makes it zero-shot.
- C: ✗ CLIP stays frozen. Only the lightweight mapping network is trained.
- D: ✗ No adversarial training.

**Q197 → A, B, D**

The annotation pipeline includes object detection, icon classification, OCR and image captioning. There is far more pretraining data than fine-tuning data. It achieves SOTA on MoTIF, Widget Captioning, MPDocVQA and WebSRC, leads ChartQA, DocVQA and InfographicVQA, and introduces new benchmarks (Screen Annotation, ScreenQA Short, Complex ScreenQA).

- A: ✓ Correct. It was trained at 670M, 2B and 5B.
- B: ✓ Correct.
- C: ✗ It is an encoder–decoder model with a ViT image encoder and an mT5/UL2 language encoder.
- D: ✓ Correct.

**Q198 → A, B, C, D**

Video frames are sampled at 1 FPS with learned temporal embeddings, then flattened. Image-causal masking lets each text token cross-attend only to the image immediately before it, while LM self-attention keeps dependencies on earlier images. Trained with up to 5 images, it generalizes to 32 at evaluation, and it adapts to new tasks by few-shot prompting without fine-tuning.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✗ The LM stays frozen. Only the new layers and the resampler are trained.

**Q199 → C**

The gate lets the model gradually learn how much visual information to inject, without disrupting the pretrained LM at the start of training. This idea of preserving pretrained knowledge while adding new conditioning recurs across multimodal models.

- A: ✗ The gate scales the whole residual contribution. It does not make attention sparse.
- B: ✗ Unrelated.
- C: ✓ Correct. tanh(0) = 0 means the new layers contribute nothing at first.
- D: ✗ The vision path is still used.

**Q200 → A, B, D**

These limits follow from its design choices: a frozen LM (inherited priors), a generative objective rather than a contrastive one (weaker retrieval and classification), and reliance on few-shot prompting.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✗ Flamingo processes video frames sampled at 1 FPS.
- D: ✓ Correct.

**Q201 → C**

Because images and text share one space, cosine similarity enables zero-shot classification, cross-modal retrieval and composed retrieval (Pic2Word). It can also be reused as the text encoder in DALL·E 2.

- A: ✗ CLIP is an embedding model, not a generator.
- B: ✗ It requires about 400M pairs.
- C: ✓ Correct.
- D: ✗ The point is a shared space.

**Q202 → D**

Learned latent queries cross-attend to the visual features. Ablations show it beats plain Transformer and MLP alternatives.

- A: ✗ The vision encoder is pretrained and frozen.
- B: ✗ The LM stays.
- C: ✗ It reduces them to a fixed number.
- D: ✓ Correct.

**Q203 → D**

NFNet-F6 is a convolutional network without batch norm; CLIP ViT is a Transformer over patches. Both are trained with the same contrastive objective. The encoder’s 2-D grid is flattened before the resampler.

- A: ✗ Different architectures.
- B: ✗ Its encoder is pretrained contrastively and then frozen.
- C: ✗ Both have image encoders.
- D: ✓ Correct.

**Q204 → A, B, D**

The query is an image plus a text modification. Strengths: zero-shot generalization, cost-effectiveness, flexibility, scalability and interpretability (images become pseudo-words).

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✗ CIR retrieves existing images from a database. It does not generate.
- D: ✓ Correct.

**Q205 → A**

The seven shift datasets vary pose, background and renditions. Fine-tuning CLIP on ImageNet reduces this robustness.

- A: ✓ Correct.
- B: ✗ It narrowed it.
- C: ✗ Too small.
- D: ✗ Not completely.

**Q206 → C**

The critical factors: compute and cost, scale of data, and the technical expertise for distributed systems and GPU management.

- A: ✗ It takes thousands of GPUs and months.
- B: ✗ Private-domain data is scarce.
- C: ✓ Correct.
- D: ✗ They are growing rapidly.

**Q207 → C**

logits = scaled cosine similarity of image and text embeddings, shape (n_images, n_texts) = (2, 3). The softmax over texts gives class probabilities with no training on these classes.

- A: ✗ logits_per_image has one row per image and one column per text.
- B: ✗ CLIP gives image-level similarities only.
- C: ✓ Correct.
- D: ✗ No loss is computed here.

**Q208 → B**

Positives sit on the diagonal (labels = arange(N)) and every other entry in the row and column is a negative. It is the same idea as NT-Xent in SimCLR, but across two modalities.

- A: ✗ No.
- B: ✓ Correct. Both encoders get a retrieval signal.
- C: ✗ The matrix is already N × N.
- D: ✗ The temperature is a separate learned scalar.

**Q209 → C**

Next, the patches are reshaped to (B, 196, 768), linearly projected to d_model, a learnable [class] token is prepended, and learnable 1-D position embeddings are added.

- A: ✗ That would be 32×32 patches.
- B: ✗ The patch size is 16, so there are 224/16 = 14 patches per side.
- C: ✓ Correct. 16·16·3 = 768 values per patch; 196 patches plus [class] = 197.
- D: ✗ It returns one vector per patch.

**Q210 → C**

This is Flamingo’s GATED XATTN-DENSE layer. The vision-conditioned path is added through a learnable tanh gate, so pretrained text ability is kept at the start and visual information is mixed in only as it becomes useful.

- A: ✗ The residual y passes through untouched.
- B: ✗ tanh(0) = 0 cancels their output.
- C: ✓ Correct. The gate opens gradually as α is learned.
- D: ✗ No.


---

## Class 7 · Diffusion Models

**Q211.** ☐ *Select all that apply.* Which statements describe denoising diffusion models (Ho et al., 2020)? Select all that apply.

- ☐ **A.** Like VAEs, they are trained by maximizing a lower bound (ELBO) on the likelihood
- ☐ **B.** All learned parameters live in the decoder (reverse process)
- ☐ **C.** The forward process is fixed and gradually blends data with noise
- ☐ **D.** The latent variables z₁…z_T have the same dimensions as the data x
- ☐ **E.** The forward process is learned jointly with the decoder, as the encoder of a VAE is

**Q212.** ○ *Single answer.* The forward process is z_t = √(1 − β_t) · z_{t−1} + √β_t · ε_t. What do the two terms do?

- ○ **A.** The first adds noise and the second removes it
- ○ **B.** The first rotates the data and the second rescales it so that the total norm stays unchanged
- ○ **C.** The first attenuates the current signal; the second adds fresh Gaussian noise
- ○ **D.** Both terms add noise, while β_t is learned by backpropagation so that the forward process can adapt to the data

**Q213.** ○ *Single answer.* What is the diffusion kernel q(z_t | x), and why is it useful?

- ○ **A.** The learned reverse distribution, which must be computed by running all t intermediate steps sequentially
- ○ **B.** A small neural network trained alongside the decoder to predict z_t from x at each step
- ○ **C.** A uniform distribution over noise levels, used to choose which timestep each training example gets
- ○ **D.** A closed-form Gaussian N(√α_t · x, (1 − α_t) I) with α_t = ∏(1 − β_s); it samples z_t in one step

**Q214.** ☐ *Select all that apply.* Reverse conditionals in diffusion models. Which statements are correct? Select all that apply.

- ☐ **A.** Each reverse step is approximated by a Gaussian with a network mean and fixed variance
- ☐ **B.** q(z_{t−1} | z_t) is generally intractable, because it requires the complex marginal q(z_{t−1})
- ☐ **C.** The normal approximation to the reverse step is reasonable only when β_t is large and T is small
- ☐ **D.** q(z_{t−1} | z_t, x), conditioned on the original data, is Gaussian with a closed form

**Q215.** ○ *Single answer.* Ho et al. reparameterized the training target. Instead of predicting z_{t−1}, the network predicts

- ○ **A.** the noise ε that was added, giving a simpler loss that works better
- ○ **B.** the noise schedule β_t, which the network learns to set separately for each training image and each step
- ○ **C.** the class label of the image
- ○ **D.** the original image x directly, in a single step from any z_t

**Q216.** ☐ *Select all that apply.* Which statements about the U-Net used in diffusion models are correct? Select all that apply.

- ☐ **A.** A separate U-Net is trained for every one of the T = 1,000 timesteps, with no time embedding
- ☐ **B.** It is used because its output has the same shape as its input, matching the predicted noise
- ☐ **C.** Downsampling cuts spatial size and adds channels; upsampling reverses it
- ☐ **D.** Encoder features are concatenated to matching decoder stages through skip connections
- ☐ **E.** A single network serves all time steps, given a sinusoidal time (noise-level) embedding

**Q217.** ○ *Single answer.* In Ho et al. (2020), what noise schedule was used, and what did later work find?

- ○ **A.** β_t linear from 0.0001 to 0.02; a later paper found a cosine schedule worked better
- ○ **B.** β_t decreasing from 0.02 down to 0.0001, so that the largest noise steps happen first; later work kept this unchanged
- ○ **C.** A learned schedule from the start
- ○ **D.** A constant β = 0.5 for all steps; later work found a linear schedule better

**Q218.** ☐ *Select all that apply.* A sampler takes 20 steps, although training used 1,000 noise levels. Which statements are correct? Select all that apply.

- ☐ **A.** The number of sampling steps can be far smaller than the number of training steps
- ☐ **B.** Sampling must run exactly 1,000 steps, because the U-Net only knows the noise levels it saw during training
- ☐ **C.** With σ_t = 0 at every step (DDIM), the same input noise always yields the same output
- ☐ **D.** Each step predicts the noise, estimates x₀, then re-noises that estimate to the t − 1 level

**Q219.** ○ *Single answer.* Why is spherical interpolation, rather than plain linear interpolation, used between two Gaussian noise tensors a and b?

- ○ **A.** Spherical interpolation removes the need to run the reverse denoising process for the in-between images
- ○ **B.** It produces images from different classes, which helps cover the whole data distribution
- ○ **C.** It keeps the noise variance constant, so every interpolant still looks like N(0, I) noise
- ○ **D.** Linear interpolation is not differentiable

**Q220.** ☐ *Select all that apply.* Two approaches to conditional generation were described. Which statements are correct? Select all that apply.

- ☐ **A.** Both approaches require retraining a separate diffusion model for each class that needs to be generated
- ☐ **B.** Classifier guidance adds a classifier gradient term to steer toward class c
- ☐ **C.** Classifier-free guidance embeds the class in the U-Net, trained with and without it
- ☐ **D.** Classifier-free guidance allows a continuous quality–diversity trade-off by weighting the conditioning

**Q221.** ○ *Single answer.* How does diffusion training handle the intractable likelihood P(x) = ∫ P(x, z₁…z_T) dz?

- ○ **A.** It lower-bounds the log-likelihood with Jensen’s inequality and maximizes the ELBO
- ○ **B.** It computes the integral exactly with Monte Carlo over all paths
- ○ **C.** It replaces the likelihood with an adversarial loss from a discriminator that tells real images from denoised ones
- ○ **D.** It ignores the likelihood and uses only perceptual loss

**Q222.** ☐ *Select all that apply.* Which statements about Sora (“Video generation models as world simulators”) are correct? Select all that apply.

- ☐ **A.** It reliably models physics, such as glass shattering, and correctly updates object state after actions like eating
- ☐ **B.** Videos are compressed into a latent space and cut into spacetime patches that act as transformer tokens
- ☐ **C.** Emergent abilities include 3D consistency and long-range coherence (object permanence)
- ☐ **D.** It is a diffusion transformer that predicts clean patches from noisy ones, conditioned on text
- ☐ **E.** It trains on native resolutions, durations and aspect ratios instead of cropping to a fixed size

**Q223.** ○ *Single answer.* A network receives z_t (an image noised to level t) and is trained to output something close to z_{t−1}. Which part of diffusion training is this?

- ○ **A.** Learning each reverse step: from a t-step-noised image, predict the (t−1)-step version
- ○ **B.** Training a discriminator that distinguishes scribbled copies from clean originals, as in adversarial training
- ○ **C.** Computing the marginal distribution q(z_t)
- ○ **D.** Training the forward process to add the right amount of noise for each individual image

**Q224.** ○ *Single answer.* What does the marginal q(z_t) represent?

- ○ **A.** The distribution of z_t over all starting data points and all diffusion paths
- ○ **B.** The distribution of one particular training image after it has been noised for t steps
- ○ **C.** A delta function at zero, since every diffusion path eventually reaches the origin
- ○ **D.** The learned reverse distribution produced by the U-Net at step t, after training has converged on the data

**Q225.** ○ *Single answer.* With T = 100 and β = 0.03 at every step, what happens to three different 1-D starting values x as they pass through z₁…z₁₀₀?

- ○ **A.** They stay exactly at their starting values, because the noise added at each step has a mean of exactly zero
- ○ **B.** They move apart without bound because noise accumulates
- ○ **C.** They drift noisily toward zero, and their paths become indistinguishable from N(0, 1)
- ○ **D.** They converge to the mean of the data distribution

**Q226.** ☐ *Select all that apply.* Which statements about generating a sample from a trained diffusion model are correct? Select all that apply.

- ☐ **A.** Repeatedly sample z_{t−1} from N(f_t[z_t, φ_t], σ_t² I) down to x (ancestral sampling)
- ☐ **B.** Start by drawing z_T from a standard normal
- ☐ **C.** Generation is iterative and therefore slower than a single VAE or GAN decoder pass
- ☐ **D.** Start from a real training image and add noise until it matches the target class
- ☐ **E.** The forward noising process must be run first on a training image to produce the starting latent

**Q227.** ○ *Single answer.* With a linear schedule β from 0.0001 to 0.02 over T = 1,000 steps, why are early steps small?

- ○ **A.** Early steps destroy little detail; bigger steps are fine once the image is noisy
- ○ **B.** To save memory
- ○ **C.** To make the forward process learnable
- ○ **D.** Because the U-Net is only trained on the first 10 steps, so later steps never need a gradient signal

**Q228.** ○ *Single answer.* In a DDIM step, which estimate is computed first from the network’s noise prediction ε̂?

- ○ **A.** The class label of the image, so that the sampler can pick the right noise schedule for it
- ○ **B.** The KL divergence
- ○ **C.** The predicted clean image x̂₀ = (x_t − √(1−ᾱ_t) ε̂) / √ᾱ_t
- ○ **D.** The next noise sample to add

**Q229.** ☐ *Select all that apply.* Which of these belong to a standard Keras diffusion-model training setup? Select all that apply.

- ☐ **A.** The AdamW optimizer, which is Adam with decoupled weight decay
- ☐ **B.** Normalization statistics computed on the training set
- ☐ **C.** A mean absolute error loss on the predicted noise
- ☐ **D.** A discriminator network trained jointly with the U-Net to sharpen the generated samples

**Q230.** ○ *Single answer.* How does the cascaded text-to-image diffusion system reach 1024×1024 output?

- ○ **A.** By tiling 256 separate 64×64 images
- ○ **B.** A GAN upsamples the 64×64 output, after the diffusion model has fixed the overall composition
- ○ **C.** 64×64 base, then 256 and 1024 stages, each conditioned on text and the smaller image
- ○ **D.** One U-Net directly generates 1024×1024

**Q231.** ○ *Single answer.* How does Sora generate images up to 2048×2048?

- ○ **A.** By upscaling with a CNN
- ○ **B.** With a separate image-only diffusion model
- ○ **C.** By generating a long video and averaging every frame into one still picture at the end
- ○ **D.** By arranging noise patches in a spatial grid one frame long

**Q232.** ○ *Single answer.* In this cosine schedule, why is signal_rates² + noise_rates² = 1 for every diffusion time?

```python
def offset_cosine_diffusion_schedule(diffusion_times):
    start_angle = tf.acos(0.95)
    end_angle = tf.acos(0.02)
    angles = start_angle + diffusion_times * (end_angle - start_angle)
    signal_rates = tf.cos(angles)
    noise_rates = tf.sin(angles)
    return noise_rates, signal_rates
```

- ○ **A.** To make the noise rate decrease over time
- ○ **B.** To make the reverse process deterministic, which is what DDIM sampling requires at every step
- ○ **C.** It is a coincidence of the chosen angles
- ○ **D.** To keep noisy images at unit variance at every noise level

**Q233.** ☐ *Select all that apply.* Read this diffusion train_step. Which statements are correct? Select all that apply.

```python
diffusion_times = tf.random.uniform(shape=(batch_size, 1, 1, 1), minval=0.0, maxval=1.0)
noise_rates, signal_rates = self.diffusion_schedule(diffusion_times)
noisy_images = signal_rates * images + noise_rates * noises
with tf.GradientTape() as tape:
    pred_noises = self.network([noisy_images, noise_rates**2], training=True)
    noise_loss = self.loss(noises, pred_noises)
```

- ☐ **A.** noisy_images is drawn in one shot from the diffusion kernel, without looping over t
- ☐ **B.** The network’s target is the added noise, and the loss compares it with the prediction
- ☐ **C.** Gradients flow into the noise schedule, so the signal and noise rates are learned along with the U-Net weights
- ☐ **D.** Each image gets its own random diffusion time in [0, 1)
- ☐ **E.** The network receives noise_rates² as its second input, which acts as the time or noise-level embedding

**Q234.** ○ *Single answer.* What does pred_images represent in this denoise function?

```python
def denoise(self, noisy_images, noise_rates, signal_rates, training):
    pred_noises = self.network([noisy_images, noise_rates**2], training=training)
    pred_images = (noisy_images - noise_rates * pred_noises) / signal_rates
    return pred_noises, pred_images
```

- ○ **A.** An estimate of the clean image x₀, from inverting x_t = s·x₀ + n·ε
- ○ **B.** The noise that should be added at the next step of the forward process, scaled by the signal rate
- ○ **C.** A sample from the prior N(0, I)
- ○ **D.** The image one step less noisy, x_{t−1}

**Q235.** ☐ *Select all that apply.* Read this reverse-diffusion loop. Which statements are correct? Select all that apply.

```python
current_images = initial_noise
step_size = 1.0 / diffusion_steps
for step in range(diffusion_steps):
    diffusion_times = tf.ones((num_images, 1, 1, 1)) - step * step_size
    noise_rates, signal_rates = self.diffusion_schedule(diffusion_times)
    pred_noises, pred_images = self.denoise(current_images, noise_rates, signal_rates, training=False)
    next_noise_rates, next_signal_rates = self.diffusion_schedule(diffusion_times - step_size)
    current_images = next_signal_rates * pred_images + next_noise_rates * pred_noises
```

- ☐ **A.** No fresh random noise is added inside the loop, so it is deterministic DDIM sampling
- ☐ **B.** diffusion_steps must equal the 1,000 noise levels used in training, or the model fails
- ☐ **C.** It starts from pure Gaussian noise
- ☐ **D.** Each step re-noises x̂₀ to the next, lower noise level using the predicted noise

**Q236.** ○ *Single answer.* With this linear DDPM schedule, what is roughly alpha_bars[-1], and what does it tell you?

```python
betas = np.linspace(1e-4, 0.02, 1000)
alphas = 1.0 - betas
alpha_bars = np.cumprod(alphas)
print(alpha_bars[-1])
```

- ○ **A.** About 0.5: half the signal survives
- ○ **B.** Exactly 0, because cumprod of numbers below 1 always reaches 0 after enough terms in floating point
- ○ **C.** About 4e−5: signal rate √ᾱ ≈ 0.006, so x_T is essentially pure noise
- ○ **D.** 0.98, since 1 − 0.02

**Q237.** ○ *Single answer.* The Keras diffusion model adapts a Normalization layer to the training images and calls this denormalize function before display. Why?

```python
self.normalizer = layers.Normalization()
model.normalizer.adapt(train_images)

def denormalize(self, images):
    images = self.normalizer.mean + images * self.normalizer.variance**0.5
    return tf.clip_by_value(images, 0.0, 1.0)
```

- ○ **A.** To make the diffusion process learnable
- ○ **B.** To remove the noise from generated images, which is an extra denoising step the U-Net cannot do itself
- ○ **C.** Train on unit-variance images to match the noise; map outputs back to pixels
- ○ **D.** To convert the images to grayscale


### Answer key — Class 7 · Diffusion Models

**Q211 → A, B, C, D**

Diffusion models are easy to train and produce samples that can exceed GAN realism. Generation draws z_T from N(0, I) and passes it through the learned decoder step by step.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct. This differs from VAEs, whose latent is lower-dimensional.
- E: ✗ The forward process has no learned parameters. Its noise schedule is a hyperparameter.

**Q212 → C**

The forward process is a Markov chain: q(z_t | z_{t−1}) = N(√(1 − β_t) z_{t−1}, β_t I). If z_{t−1} has unit variance, Var(z_t) = (1 − β_t) + β_t = 1, so variance is preserved while signal is replaced by noise. After enough steps, q(z_T | x) ≈ N(0, I).

- A: ✗ Neither term removes noise.
- B: ✗ Not rotation.
- C: ✓ Correct.
- D: ✗ β_t is a fixed noise schedule, not learned.

**Q213 → D**

As t grows, the mean √α_t x shrinks toward zero and the variance 1 − α_t grows toward 1, so the kernel approaches a standard normal. Training uses it to jump directly to any noise level for a training image, the same reparameterization idea as a VAE: z_t = √α_t x + √(1 − α_t) ε.

- A: ✗ The kernel is the forward shortcut that avoids running the intermediate steps.
- B: ✗ It is an analytic distribution, not a network.
- C: ✗ It is Gaussian.
- D: ✓ Correct.

**Q214 → A, B, D**

By Bayes’ rule, q(z_{t−1} | z_t) ∝ q(z_t | z_{t−1}) q(z_{t−1}). This is often well approximated by a normal distribution, but not always. Conditioning on x makes every factor Gaussian, so the training target is exact.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✗ It is reasonable when β_t is small (close to 0) and T is large.
- D: ✓ Correct. Its mean blends z_t and x.

**Q215 → A**

The loss becomes a least-squares error between the true and predicted noise (mean absolute error also works in practice). Predicting the noise is an easier learning task, and the noise has the same shape as the image, which is why a U-Net is used.

- A: ✓ Correct. The loss compares ε̂ = g_t(z_t, φ) with the true ε.
- B: ✗ β_t is fixed.
- C: ✗ Unconditional DDPMs do not predict labels.
- D: ✗ Predicting the clean image is possible, but it is not the DDPM reparameterization.

**Q216 → B, C, D, E**

Residual blocks connect adjacent representations, with periodic global self-attention. In a typical Keras implementation, each DownBlock has two residual blocks and average pooling, and each UpBlock has bilinear upsampling, concatenation of skips, and two residual blocks.

- A: ✗ One shared network is conditioned on t. Separate networks would multiply the parameters by 1,000 and share no knowledge between noise levels.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✓ Correct.

**Q217 → A**

Increasing β_t means early steps destroy little detail. Nichol & Dhariwal’s cosine schedule spreads signal destruction more evenly. In terms of ᾱ_t, √ᾱ_t is the signal rate and √(1 − ᾱ_t) is the noise rate.

- A: ✓ Correct.
- B: ✗ The schedule increases: small steps early, larger ones once the image is already noisy.
- C: ✗ The DDPM schedule was fixed and linear.
- D: ✗ Neither part is right.

**Q218 → A, C, D**

Song et al. (2020) DDIM equation: x_{t−1} = √ᾱ_{t−1} · x̂₀ + √(1 − ᾱ_{t−1} − σ_t²) · ε̂ + σ_t ε. A deterministic mapping gives a well-defined correspondence between latent noise and images, which is useful for interpolation.

- A: ✓ Correct.
- B: ✗ The time embedding is continuous, and DDIM-style updates allow skipping levels.
- C: ✓ Correct. DDIM sampling is deterministic.
- D: ✓ Correct. This is the two-step jump from x_t to x_{t−1}.

**Q219 → C**

A linear midpoint (a + b)/2 of independent standard normals has variance 0.5, which is off-distribution for the denoiser. The sin/cos weights satisfy sin² + cos² = 1, preserving unit variance. With deterministic DDIM sampling this gives smooth image transitions.

- A: ✗ Every interpolant still has to be denoised by the model.
- B: ✗ Not its purpose.
- C: ✓ Correct. For example, sin(πt/2)·a + cos(πt/2)·b.
- D: ✗ It is differentiable.

**Q220 → B, C, D**

Text-to-image systems (e.g., Imagen, Saharia et al. 2022) condition on a sentence embedding from a large language model and use a cascade: 64×64 base → 256×256 → 1024×1024 super-resolution, each stage conditioned on the text and the lower-resolution image.

- A: ✗ One model handles all classes in both approaches.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.

**Q221 → A**

The loss has a reconstruction term (recovering x from z₁) and diffusion terms (matching each predicted z_{t−1} to the Gaussian target from q(z_{t−1} | z_t, x)). It is summed over data points and steps. In practice: sample a time step, diffuse with the kernel, and update the decoder.

- A: ✓ Correct.
- B: ✗ The integral cannot be computed exactly.
- C: ✗ Diffusion models are not adversarial.
- D: ✗ Training is likelihood-based.

**Q222 → B, C, D, E**

Sample quality improves markedly with compute (base → 4× → 32×). GPT expands short prompts into detailed captions. Sora animates images, extends videos, loops, does SDEdit-based editing and interpolation, and generates images up to 2048×2048 using a one-frame spatial grid.

- A: ✗ These are known limitations. Physics and object-state changes are often wrong, because nothing in a patch-level denoising loss enforces conservation laws.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✓ Correct.

**Q223 → A**

The reverse step is the only learned part. The training pair (z_t, target) comes from the fixed forward process. The exact target is q(z_{t−1} | z_t, x), a Gaussian with closed form (see the code, where a brute-force simulation matches the formula). Generation starts from N(0, I) and applies the learned step for t = T…1. In practice one U-Net conditioned on t does every step, and it predicts ε rather than z_{t−1}.

- A: ✓ Correct.
- B: ✗ No discriminator is involved.
- C: ✗ The marginal is a separate idea (the overall distribution of scribbled photos).
- D: ✗ The forward process (scribbling) is fixed. Only denoising is learned.

**Q224 → A**

q(z_t) = ∫ q(z_t | x) Pr(x) dx. It is the distribution you would get by noising every training image to level t and pooling the results. As t grows it blurs Pr(x) toward N(0, I). In a fitted model, the estimated marginals closely match these true marginals.

- A: ✓ Correct.
- B: ✗ That is the kernel q(z_t | x).
- C: ✗ It is a broad distribution.
- D: ✗ That is the model’s estimate, p(z_t).

**Q225 → C**

Each step multiplies by √0.97 ≈ 0.985 and adds noise with variance 0.03. The conditionals q(z_t | z_{t−1}) are normal, with a mean slightly closer to zero than the current point and fixed variance β_t.

- A: ✗ Zero-mean noise still spreads the values, and attenuation shrinks the mean toward zero.
- B: ✗ Attenuation by √(1 − β) keeps the variance bounded.
- C: ✓ Correct.
- D: ✗ They converge to the standard normal, centered at 0, not to the data mean.

**Q226 → A, B, C**

Speed-ups: deterministic DDIM updates that jump between noise levels, so about 20 steps can replace 1,000 (see the DDIM code). Conditioning (class, image, text) can be added at every denoising step.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✗ That is closer to SDEdit-style editing. Unconditional generation starts from pure noise.
- E: ✗ Generation does not need any training image. z_T comes straight from the prior.

**Q227 → A**

A cosine schedule later improved on this by spreading the destruction of signal more evenly.

- A: ✓ Correct.
- B: ✗ Not the reason.
- C: ✗ It is fixed.
- D: ✗ All timesteps are trained.

**Q228 → C**

Then x_{t−1} = √ᾱ_{t−1} x̂₀ + √(1 − ᾱ_{t−1}) ε̂ (when σ = 0): the signal is rescaled to the t−1 rate and the predicted noise reapplied at the t−1 noise rate.

- A: ✗ No labels are involved.
- B: ✗ Not computed during sampling.
- C: ✓ Correct.
- D: ✗ Fresh noise is only added when σ_t > 0.

**Q229 → A, B, C**

The model was trained for 50 epochs. DownBlocks use average pooling; UpBlocks use bilinear upsampling plus concatenated skips.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✗ No discriminator is used.

**Q230 → C**

The text is encoded by a large language model (Saharia et al., 2022). The stochastic model yields many compatible images and can count objects and render text.

- A: ✗ Not tiling.
- B: ✗ All stages are diffusion models.
- C: ✓ Correct.
- D: ✗ It uses a cascade.

**Q231 → D**

Video size is controlled at inference by arranging randomly initialized patches in a grid of the right size. Images are simply one-frame videos.

- A: ✗ Not described.
- B: ✗ The same model is used.
- C: ✗ Not how it works.
- D: ✓ Correct.

**Q232 → D**

x_t = signal·x₀ + noise·ε with Var(x₀) = Var(ε) = 1 (after normalization). Then Var(x_t) = signal² + noise² = 1. The offset keeps the signal rate below 0.95 at t = 0 and the noise rate below 1 until the end, which avoids degenerate steps.

- A: ✗ The noise rate increases from about 0.31 to 1.0 as t goes from 0 to 1.
- B: ✗ Determinism comes from DDIM with σ = 0, not from the schedule.
- C: ✗ It holds for any angle, since cos² + sin² = 1.
- D: ✓ Correct. The variance-preserving property.

**Q233 → A, B, D, E**

This is the whole DDPM/DDIM training loop: sample x₀, t and ε; form x_t = s(t)·x₀ + n(t)·ε; regress ε̂(x_t, t) onto ε. Foster uses mean absolute error with AdamW.

- A: ✓ Correct.
- B: ✓ Correct. This is the ε-prediction reparameterization.
- C: ✗ The schedule is a fixed function with no trainable variables.
- D: ✓ Correct. All noise levels are trained in every batch.
- E: ✓ Correct. One U-Net serves every noise level.

**Q234 → A**

Solving x_t = s·x₀ + n·ε for x₀ gives x̂₀ = (x_t − n·ε̂)/s. It can be blurry at high noise, which is why sampling re-noises it and repeats over many steps.

- A: ✓ Correct.
- B: ✗ pred_noises is the noise estimate. pred_images is the clean estimate.
- C: ✗ No.
- D: ✗ The formula inverts the whole kernel, so it estimates x₀.

**Q235 → A, C, D**

Each step: (1) predict noise and x̂₀ at time t; (2) move to t − 1/steps; (3) set x_{t−Δ} = s(t−Δ)·x̂₀ + n(t−Δ)·ε̂. Fewer steps run faster at slightly lower quality.

- A: ✓ Correct. The same initial_noise always gives the same image.
- B: ✗ Times are continuous, so any number of steps (e.g., 20) works.
- C: ✓ Correct. initial_noise ~ N(0, I).
- D: ✓ Correct.

**Q236 → C**

ᾱ_t = ∏(1 − β_s) is the fraction of signal variance left. Training samples t uniformly and uses √ᾱ_t·x₀ + √(1 − ᾱ_t)·ε. Generation can start from N(0, I) only because ᾱ_T is about 0.

- A: ✗ Far too large.
- B: ✗ It is tiny but not exactly 0 (4.04e−5).
- C: ✓ Correct. q(x_T | x₀) ≈ N(0, I).
- D: ✗ That is a single step’s α, not the cumulative product.

**Q237 → C**

The variance-preserving schedule assumes Var(x₀) ≈ 1. Normalizing the data makes the signal and noise terms comparable. Clipping to [0, 1] after denormalizing gives displayable pixels.

- A: ✗ No.
- B: ✗ Denormalizing is just a linear rescale. It does no denoising.
- C: ✓ Correct.
- D: ✗ Normalization does not change the channels.


---

## Cross-topic synthesis

**Q238.** ☐ *Select all that apply.* Skip or residual connections appear throughout the course. In which models do they play a central role? Select all that apply.

- ☐ **A.** The Transformer (around attention and FFN sub-layers)
- ☐ **B.** The diffusion U-Net
- ☐ **C.** ResNet
- ☐ **D.** The original single-layer perceptron, where the skip lets the input bypass its one weighted sum
- ☐ **E.** PixelCNN residual blocks

**Q239.** ○ *Single answer.* Which comparison of latent dimensionality is correct?

- ○ **A.** Autoregressive models such as PixelCNN use a 200-dimensional latent
- ○ **B.** Diffusion latents are lower-dimensional than the data, while VAE latents are larger than the input image
- ○ **C.** Both VAEs and diffusion models compress to a lower-dimensional latent
- ○ **D.** VAE latents are usually lower-dimensional than x; diffusion latents z₁…z_T match x’s size

**Q240.** ☐ *Select all that apply.* Masking appears in several architectures. Which statements are correct? Select all that apply.

- ☐ **A.** Flamingo masks cross-attention so each text token sees only the image just before it
- ☐ **B.** CLIP masks half of each image’s patches and trains the encoder to reconstruct the missing pixels
- ☐ **C.** BERT masks input tokens and predicts them from both sides (MLM)
- ☐ **D.** PixelCNN masks convolution weights so each pixel sees only earlier pixels in raster order
- ☐ **E.** Decoder self-attention masks future positions to keep generation autoregressive

**Q241.** ☐ *Select all that apply.* Contrastive objectives appear in several models. Which use a contrastive loss as a core training signal? Select all that apply.

- ☐ **A.** DDPM noise prediction, which contrasts each predicted noise vector against the noise of other images in the batch
- ☐ **B.** Pic2Word’s mapping network
- ☐ **C.** SimCLR
- ☐ **D.** CLIP
- ☐ **E.** Flamingo’s vision encoder pretraining

**Q242.** ○ *Single answer.* Which family generally needs one network pass per generated element, making sampling inherently sequential and slow for long outputs?

- ○ **A.** GANs, since the generator must be run once for each pixel that it outputs
- ○ **B.** Contrastive encoders like SimCLR
- ○ **C.** VAEs
- ○ **D.** Autoregressive models such as PixelCNN and GPT

**Q243.** ○ *Single answer.* Which statement correctly contrasts the role of the KL term in a VAE with the role of KL inside the diffusion ELBO?

- ○ **A.** Both regularize a learned encoder toward N(0, I)
- ○ **B.** VAE KL regularizes the learned encoder; diffusion KLs fit reverse steps to fixed targets
- ○ **C.** VAEs have no KL term; their loss is reconstruction only, while diffusion models add a KL for stability
- ○ **D.** Diffusion models have no KL terms at all; their loss is purely adversarial, comparing generated and real images

**Q244.** ○ *Single answer.* A researcher wants a model that can directly score how likely a new image is, with an exact (not bounded) log-likelihood. Which family from the course fits best?

- ○ **A.** Autoregressive model (e.g., PixelCNN)
- ○ **B.** Diffusion model
- ○ **C.** GAN
- ○ **D.** VAE, because its ELBO is always exactly equal to log p(x) once training has fully converged

**Q245.** ○ *Single answer.* Which pairing of model and generation step count is correct?

- ○ **A.** VAE: T denoising steps
- ○ **B.** GAN: one network pass per pixel, so a 64×64 image needs 4,096 sequential passes
- ○ **C.** PixelCNN: one pass for the whole image
- ○ **D.** DDPM: about 1,000 steps; DDIM: far fewer (e.g., 20)

**Q246.** ☐ *Select all that apply.* Which models freeze a large pretrained component and train only new connecting modules? Select all that apply.

- ☐ **A.** BLIP-2 (frozen image encoder and LLM; trains the Q-Former)
- ☐ **B.** Pic2Word (frozen CLIP; trains the mapping network)
- ☐ **C.** Flamingo (frozen NFNet and LM; trains the resampler and gated cross-attention)
- ☐ **D.** SimCLR, which freezes a supervised ImageNet encoder and only trains its projection head

**Q247.** ○ *Single answer.* What do the VAE, diffusion and Sora pipelines have in common regarding Gaussian noise?

- ○ **A.** They all use adversarial noise
- ○ **B.** Each samples standard-normal noise and maps it to data with a learned network
- ○ **C.** None use Gaussian noise
- ○ **D.** All three add noise only at training time and generate fully deterministically from fixed inputs


### Answer key — Cross-topic synthesis

**Q238 → A, B, C, E**

Skip connections ease optimization by representing identity mappings easily, mitigate vanishing gradients and degradation, and smooth the loss landscape. In U-Nets they also carry high-resolution detail from the encoder to the decoder by concatenation, not addition.

- A: ✓ Correct. They form the residual stream that MEMIT edits.
- B: ✓ Correct. There are residual blocks plus encoder–decoder skip concatenations.
- C: ✓ Correct. f(x) = C(x) + x.
- D: ✗ A single-layer perceptron has nothing to skip.
- E: ✓ Correct.

**Q239 → D**

A VAE compresses (2-D for Fashion-MNIST, 200-D for CelebA). Diffusion corrupts at full resolution, which is why generation is costly. Latent diffusion approaches, including Sora’s compressed spacetime latent, run diffusion in a learned compressed space.

- A: ✗ Autoregressive models have no latent variable; they condition on previous outputs.
- B: ✗ This is reversed.
- C: ✗ Diffusion latents keep the data dimension.
- D: ✓ Correct.

**Q240 → A, C, D, E**

Masking controls information flow. Causal masks (GPT, PixelCNN) enforce an ordering. Input masks (BERT) define a self-supervised objective. Cross-modal masks (Flamingo) control which media each token can see.

- A: ✓ Correct. This is image-causal masking.
- B: ✗ That describes masked autoencoders (MAE). CLIP is contrastive and has no reconstruction.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✓ Correct.

**Q241 → B, C, D, E**

Contrastive learning pulls positive pairs together and pushes negatives apart in an embedding space. A recurring theme: large batches or many negatives help, temperature matters, and the learned embeddings transfer well (zero-shot or linear probe).

- A: ✗ DDPM uses a per-sample regression (least-squares) loss.
- B: ✓ Correct (pseudo-token embedding versus image embedding).
- C: ✓ Correct (NT-Xent over augmented views).
- D: ✓ Correct (symmetric cross-entropy over image–text pairs).
- E: ✓ Correct (NFNet-F6 trained with a CLIP-style two-term loss).

**Q242 → D**

Sampling cost: autoregressive models take one pass per token or pixel; diffusion models take one pass per denoising step (1,000 in DDPM, about 20 with DDIM-style samplers); VAEs and GANs take a single pass. Training of autoregressive Transformers is still parallel thanks to causal masking.

- A: ✗ A GAN generator produces the whole image in one pass.
- B: ✗ These are not generators.
- C: ✗ A VAE generates with one decoder pass after sampling z.
- D: ✓ Correct.

**Q243 → B**

Both maximize an ELBO. In the VAE, both the encoder and decoder are learned. In diffusion, the encoder is fixed, so the KL terms only train the decoder to invert known Gaussian corruption steps.

- A: ✗ Diffusion has no learned encoder.
- B: ✓ Correct.
- C: ✗ The KL is half of the VAE loss.
- D: ✗ The ELBO decomposes into KL and reconstruction terms, which simplify to a noise-prediction MSE.

**Q244 → A**

This follows the Class 1 taxonomy: tractable explicit models (autoregressive, normalizing flows) give exact densities; approximate models (VAE, diffusion, EBM) give bounds or approximations; implicit models (GAN) give none.

- A: ✓ Correct. p(x) = ∏ p(x_i | x_<i) is computed exactly.
- B: ✗ Standard DDPM training also gives a bound, not the exact likelihood.
- C: ✗ GANs are implicit models and give no likelihood.
- D: ✗ The ELBO equals log p(x) only if q matches the true posterior exactly, which rarely happens.

**Q245 → D**

Speed is a key trade-off between the families: single-pass (VAE, GAN), iterative (diffusion) and sequential per element (autoregressive).

- A: ✗ A VAE needs one decoder pass.
- B: ✗ That is how an autoregressive model generates.
- C: ✗ PixelCNN needs one pass per pixel.
- D: ✓ Correct.

**Q246 → A, B, C**

Freezing keeps pretrained knowledge, cuts compute, and avoids catastrophic forgetting. This is the same principle as transfer learning in Class 2.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✗ SimCLR trains the encoder from scratch without labels.

**Q247 → B**

VAE: z ~ N(0, I) → decoder. Diffusion: z_T ~ N(0, I) → iterative denoiser. Sora: noisy spacetime latent patches → diffusion transformer.

- A: ✗ No.
- B: ✓ Correct.
- C: ✗ All three do.
- D: ✗ VAEs and DDPMs sample noise at generation time.


---

## Your homework notebooks

**Q248.** ○ *Single answer.* Class 1 latent-space notebook. The images are normalized with Normalize((0.5,), (0.5,)), and the decoder ends in nn.Sigmoid(). Training MSE stays near 0.92 for all 10 epochs. Why?

```python
transform = transforms.Compose([
    transforms.ToTensor(),                     # [0, 1]
    transforms.Normalize((0.5,), (0.5,))       # -> [-1, 1]
])
...
self.decoder = nn.Sequential(
    nn.Linear(encoding_dim, 128), nn.ReLU(True),
    nn.Linear(128, 28 * 28),
    nn.Sigmoid()                               # outputs in (0, 1)
)
criterion = nn.MSELoss()
```

- ○ **A.** The learning rate 1e-3 is too high for Adam
- ○ **B.** Targets lie in [−1, 1] but sigmoid outputs lie in (0, 1), so each black pixel at −1 costs about 1
- ○ **C.** The 64-dimensional bottleneck is too small to represent a 28×28 digit, so no reconstruction can improve
- ○ **D.** Mixed-precision autocast rounds the loss

**Q249.** ○ *Single answer.* In the same autoencoder, the encoder ends with nn.ReLU(True) right after the Linear(128, 64) bottleneck. What is a side effect on the latent codes?

```python
self.encoder = nn.Sequential(
    nn.Linear(28 * 28, 128), nn.ReLU(True),
    nn.Linear(128, encoding_dim),
    nn.ReLU(True)          # <- applied to the latent code
)
```

- ○ **A.** Latent codes can be negative, centered at zero
- ○ **B.** The latent space becomes a standard normal distribution, which makes random sampling possible
- ○ **C.** Codes are non-negative, and some dimensions can be stuck at 0 for every input (dead units)
- ○ **D.** The decoder can no longer be trained

**Q250.** ○ *Single answer.* How many learnable parameters does this encoder have?

```python
nn.Linear(28 * 28, 128), nn.ReLU(True),
nn.Linear(128, 64),      nn.ReLU(True)
```

- ○ **A.** 100,352
- ○ **B.** 108,544, since ReLU layers each add one learnable threshold for every unit they are applied to
- ○ **C.** 108,736
- ○ **D.** 217,472

**Q251.** ○ *Single answer.* Class 2 CL_Simple notebook. The pixels are already divided by 255, and the augmentation pipeline also contains Rescaling(1./255). What is the effect?

```python
x_train = x_train.astype('float32') / 255.0
data_augmentation = keras.Sequential([
    layers.RandomCrop(height=32, width=32),
    layers.RandomFlip("horizontal"),
    layers.Rescaling(1./255),       # second division by 255
    layers.RandomZoom(0.2),
])
```

- ○ **A.** Inputs become [0, 1/255]: tiny contrast, so early layers are dominated by their biases
- ○ **B.** It converts the images to grayscale, which removes the color information that SimCLR relies on most
- ○ **C.** No effect; Rescaling is skipped when values are already in [0, 1]
- ○ **D.** It reverses the earlier normalization, restoring the 0–255 range

**Q252.** ○ *Single answer.* The CL_Simple training step builds one view per image and uses labels = tf.range(batch) on the similarity matrix normalized · normalizedᵀ. What is the positive pair for image i?

```python
encoded = encoder(x_batch_train, training=True)          # ONE view per image
projected = projection_head(encoded, training=True)
normalized = tf.math.l2_normalize(projected, axis=1)
cosine_similarity = tf.matmul(normalized, normalized, transpose_b=True)
logits = cosine_similarity / temperature                  # temperature = 0.1
labels = tf.range(x_batch_train.shape[0])                 # target = diagonal
loss_value = keras.losses.sparse_categorical_crossentropy(labels, logits, from_logits=True)
```

- ○ **A.** A second augmented view of image i
- ○ **B.** Image i itself: the diagonal entry, whose cosine similarity is always 1
- ○ **C.** The next image in the batch, i + 1
- ○ **D.** The image with the same CIFAR-10 class label, chosen at random from the rest of the batch

**Q253.** ☐ *Select all that apply.* Your CL_Simple loss started near 5.5 and flattened near 0.018 (batch size 256, τ = 0.1). Which explanations are correct? Select all that apply.

```python
# loss for row i with one view and labels = range(N):
#   -log( e^{10} / (e^{10} + sum_{k != i} e^{cos_ik / 0.1}) )
import numpy as np
print(np.log(256))                       # 5.545 -> initial loss
print(np.log(1 + 255 * np.exp(-10)))     # 0.0115 -> floor
```

- ☐ **A.** ≈5.5 is log(256): at the start the softmax is close to uniform over 256 columns
- ☐ **B.** Reaching the floor shows that the encoder learned class-separating features, as the t-SNE plot should confirm
- ☐ **C.** The loss could drop further toward 0 by lowering τ, without learning anything new
- ☐ **D.** The floor ≈ 0.0115 = log(1 + 255·e^{−10}) is reached when every other embedding is orthogonal to image i

**Q254.** ○ *Single answer.* In CL_Simple, what does layers.RandomCrop(height=32, width=32) do to 32×32 CIFAR images?

```python
layers.RandomCrop(height=32, width=32)   # input is already 32x32
```

- ○ **A.** It crops the center 16×16
- ○ **B.** It pads the image to 40×40 and then crops a random 32×32 window, giving small translations
- ○ **C.** A strong random crop like SimCLR’s
- ○ **D.** Nothing: a 32×32 crop of a 32×32 image is the whole image

**Q255.** ○ *Single answer.* CL_CustomeCLFunction builds pairs with make_pairs() using class labels (same class = positive, different class = negative). How does this differ from SimCLR?

```python
idxB = np.random.choice(idx[label])                 # same class -> positive
pair_labels.append([1])
neg_image = images[np.random.choice(neg_idx)]        # other class -> negative
pair_labels.append([0])
```

- ○ **A.** It is the same as SimCLR
- ○ **B.** It is supervised (needs labels); SimCLR’s positives are two augmentations of one image
- ○ **C.** It is self-supervised, because the labels only decide which pairs are formed, not what the loss looks like
- ○ **D.** It uses 2N − 2 negatives per positive, as in SimCLR

**Q256.** ○ *Single answer.* In CL_CustomeCLFunction, the margin loss receives y_pred from Dense(1, sigmoid), not the raw distance. If the model outputs a constant 0.5 for every pair (balanced positives and negatives), what is the loss?

```python
def contrastive_loss(y_true, y_pred):
    margin = 1
    square_pred = tf.square(y_pred)
    margin_square = tf.square(tf.maximum(margin - y_pred, 0))
    return tf.reduce_mean(y_true * square_pred + (1 - y_true) * margin_square)

distance = layers.Lambda(lambda e: tf.norm(e[0] - e[1], axis=1, keepdims=True))([a, b])
outputs = layers.Dense(1, activation="sigmoid")(distance)   # y_pred in (0, 1)
```

- ○ **A.** 0.25
- ○ **B.** 0
- ○ **C.** 0.5, because the positive term p² and the negative term (1 − p)² are added rather than averaged
- ○ **D.** 1.0

**Q257.** ○ *Single answer.* The frozen ImageNet ResNet50 receives 32×32 CIFAR images with include_top=False. What spatial size reaches GlobalAveragePooling2D, and how many parameters are trainable in the whole Siamese model?

```python
base_model = applications.ResNet50(weights='imagenet', include_top=False, input_shape=(32, 32, 3))
base_model.trainable = False
x = base_model(x, training=False)
x = layers.GlobalAveragePooling2D()(x)
outputs = layers.Dense(128, activation=None)(x)
...
outputs = layers.Dense(1, activation="sigmoid")(distance)
```

- ○ **A.** 4×4×512; about 23.5 million, since setting base_model.trainable = False only freezes batch-norm statistics
- ○ **B.** 1×1×2048; 262,274
- ○ **C.** 7×7×2048; 2,048
- ○ **D.** 32×32×3; 0

**Q258.** ○ *Single answer.* Class 3 VAE notebook: why are the 28×28 Fashion-MNIST images padded to 32×32 before the encoder?

```python
imgs = np.pad(imgs, ((0, 0), (2, 2), (2, 2)), constant_values=0.0)   # 28 -> 32
x = layers.Conv2D(32,  (3, 3), strides=2, padding="same")(encoder_input)  # 16
x = layers.Conv2D(64,  (3, 3), strides=2, padding="same")(x)              # 8
x = layers.Conv2D(128, (3, 3), strides=2, padding="same")(x)              # 4
```

- ○ **A.** To add a border that helps the KL term
- ○ **B.** Because Conv2D layers in Keras refuse to accept inputs whose height and width are not powers of two
- ○ **C.** 32 halves cleanly three times (32→16→8→4), so the decoder’s three ×2 upsamplings return exactly 32
- ○ **D.** To center the clothing items

**Q259.** ○ *Single answer.* In your VAE, BETA = 500 multiplies the reconstruction loss, not the KL loss. Relative to an unweighted sum, what does this do?

```python
reconstruction_loss = tf.reduce_mean(
    BETA * losses.binary_crossentropy(data, reconstruction, axis=(1, 2, 3)))
kl_loss = tf.reduce_mean(tf.reduce_sum(
    -0.5 * (1 + z_log_var - tf.square(z_mean) - tf.exp(z_log_var)), axis=1))
total_loss = reconstruction_loss + kl_loss
```

- ○ **A.** It changes the reparameterization trick, scaling ε by 500 so that the sampled latent codes spread more widely
- ○ **B.** It strengthens the KL regularization
- ○ **C.** Reconstruction dominates (like KL weight 1/500): sharper outputs, looser prior fit
- ○ **D.** It has no effect, because Adam normalizes the gradient scale of each parameter separately

**Q260.** ○ *Single answer.* In the Sampling layer, why is the noise multiplied by tf.exp(0.5 * z_log_var)?

```python
class Sampling(layers.Layer):
    def call(self, inputs):
        z_mean, z_log_var = inputs
        epsilon = K.random_normal(shape=(tf.shape(z_mean)[0], tf.shape(z_mean)[1]))
        return z_mean + tf.exp(0.5 * z_log_var) * epsilon
```

- ○ **A.** It is the variance σ²
- ○ **B.** It is σ = √(e^{log σ²}), and the reparameterization needs the standard deviation
- ○ **C.** It is a learning-rate warmup factor applied to the latent noise during the first few epochs
- ○ **D.** It keeps the KL term at zero

**Q261.** ☐ *Select all that apply.* Your VAE run had two quiet bugs that you spotted. Which statements are correct? Select all that apply.

```python
model_checkpoint_callback = callbacks.ModelCheckpoint(..., monitor="loss", save_best_only=True)
return {m.name: m.result() for m in self.metrics}   # names: total_loss, reconstruction_loss, kl_loss

x = norm.ppf(np.linspace(0, 1, grid_size))           # includes ppf(0) and ppf(1)
p = norm.cdf(z)
```

- ☐ **A.** norm.ppf(0) = −∞ and ppf(1) = +∞, so the grid’s outer ring decodes from infinite points
- ☐ **B.** norm.cdf(z) maps N(0, 1) codes to Uniform(0, 1), so an even spread means z fits the prior
- ☐ **C.** ModelCheckpoint monitors "loss", but train_step returns "total_loss", so no checkpoint is saved
- ☐ **D.** The reconstruction loss should use mean squared error because binary cross-entropy is undefined on padded pixels

**Q262.** ○ *Single answer.* Class 4 BertViz notebook. For sentence_a = “The cat sat on the mat” and sentence_b = “The cat lay on the rug”, how many tokens are there, and what is sentence_b_start?

```python
inputs = tokenizer(sentence_a, sentence_b, return_tensors='pt')
token_type_ids = inputs['token_type_ids']
sentence_b_start = token_type_ids[0].tolist().index(1)
```

- ○ **A.** 12 tokens; 6
- ○ **B.** 13 tokens; 7
- ○ **C.** 15 tokens; 8
- ○ **D.** 14 tokens; 7, because BERT uses only one [SEP] token between the sentences and none at the end

**Q263.** ○ *Single answer.* outputs.attentions is a tuple of 12 tensors. After A = torch.stack(attention)[:, 0], what is A’s shape, and what is A[L, h, i, j]?

```python
A = torch.stack(attention)[:, 0]
def next_tok(L, h):
    return torch.stack([A[L, h, i, i+1] for i in range(n-1)]).mean().item()
```

- ○ **A.** (15, 15); the average over all layers and heads
- ○ **B.** (12, 15, 15); attention from token j to token i
- ○ **C.** (1, 12, 12, 15); the value vector of token i in head h, as produced by the W_V projection
- ○ **D.** (12, 12, 15, 15); how much token i attends to j in layer L, head h

**Q264.** ○ *Single answer.* You found layer 2, heads 0 and 9 put about 0.86 of their attention on the next token. Why could this pattern never appear in GPT-2?

```python
print("L2 H0 next-token:", round(next_tok(2, 0), 2))   # 0.86
print("L3 H5 prev-token:", round(prev_tok(3, 5), 2))   # 0.61
```

- ○ **A.** GPT-2 uses learned positional embeddings, which cannot represent a relative offset of one token
- ○ **B.** GPT-2’s causal mask zeroes every weight on future positions, including i+1
- ○ **C.** GPT-2 has only one attention head per layer
- ○ **D.** GPT-2 has fewer layers

**Q265.** ○ *Single answer.* From layer 4 onward, 0.60–0.74 of all attention lands on the two [SEP] tokens. What is the usual interpretation?

```python
for L in range(12):
    print(f"layer {L}: CLS {A[L,:,:,0].mean():.2f}  SEP {A[L,:,:,sep].sum(-1).mean():.2f}")
```

- ○ **A.** The model is copying the sentence boundary into every token’s value vector to improve NSP
- ○ **B.** A bug in BertViz that mislabels the [CLS] token as [SEP] when two sentences are given together
- ○ **C.** A “no-op” sink: heads with nothing to attend to park their weight on [SEP]
- ○ **D.** [SEP] holds the most semantic content in the sentence


### Answer key — Your homework notebooks

**Q248 → B**

The best a sigmoid can output for target −1 is about 0, giving squared error (0 − (−1))² = 1 per black pixel. Fix either side: drop the Normalize (keep [0, 1]), or use Tanh as the last activation. A second point: the printed loss is the last batch’s, because the print is outside the inner loop, so the epoch-to-epoch wiggle is just noise.

- A: ✗ A too-high LR gives unstable or exploding loss, not a flat floor.
- B: ✓ Correct. MNIST is about 80% black pixels, so the loss floor is near 0.8–0.9.
- C: ✗ 64 dimensions is plenty for MNIST. A plain AE reaches far lower error once the ranges match.
- D: ✗ fp16 rounding is far too small to explain a floor of 0.9.

**Q249 → C**

A ReLU at the bottleneck throws away half of each dimension’s range and can kill units whose pre-activation is always negative. Autoencoders usually leave the bottleneck linear. Either way, a plain AE’s codes are not a distribution you can sample from, which is what a VAE adds.

- A: ✗ ReLU clips negatives to 0.
- B: ✗ Only a VAE’s KL term does that. A ReLU bottleneck does the opposite.
- C: ✓ Correct. You can see many exact zeros in the printed latent vectors.
- D: ✗ It trains, with a constrained code.

**Q250 → C**

A Linear(in, out) layer has in·out weights plus out biases. ReLU, Flatten and Sigmoid have none. The decoder is 64·128 + 128 + 128·784 + 784 = 109,456.

- A: ✗ This counts only the first layer’s weights (784·128) and omits everything else.
- B: ✗ ReLU has no parameters, and this also drops the biases.
- C: ✓ Correct. (784·128 + 128) + (128·64 + 64) = 100,480 + 8,256.
- D: ✗ That doubles the count, as if the decoder were included twice.

**Q251 → A**

Unlike RandomFlip or RandomZoom, Rescaling is deterministic and active at inference too. The network can partly compensate with larger weights, but optimization becomes harder. Remove one of the two scalings.

- A: ✓ Correct. It is also applied in encoder.predict, not only during training.
- B: ✗ Rescaling changes scale, not channels.
- C: ✗ Rescaling always multiplies. It does not check the input range.
- D: ✗ Multiplying by 1/255 again shrinks further.

**Q252 → B**

Since sim(i, i) = 1 always, the loss is minimized just by pushing different images apart. Nothing forces invariance to augmentation, which is the whole point of SimCLR. The fix: encode two augmentations per image (2N rows), mask the diagonal, and use partner indices i ± N as labels. The NT-Xent code panel shows exactly this.

- A: ✗ No second view is ever created. Each image passes through the encoder once.
- B: ✓ Correct. The ‘positive’ is trivially satisfied.
- C: ✗ tf.range(batch) makes label i point at column i.
- D: ✗ Class labels are not used in this notebook.

**Q253 → A, C, D**

A low contrastive loss is not proof of a good representation. The SimCLR paper makes the same point: without ℓ2 normalization, contrastive accuracy rose while linear-evaluation accuracy fell. Judge representations with a downstream probe (linear evaluation or k-NN), not with the pretext loss.

- A: ✓ Correct. log(256) = 5.545.
- B: ✗ The loss can hit the floor by spreading embeddings apart arbitrarily. Your t-SNE showed no class clusters, which is consistent with that.
- C: ✓ Correct. A smaller τ raises the diagonal logit, which shrinks the floor.
- D: ✓ Correct. The diagonal logit is 1/τ = 10 and the others are about 0.

**Q254 → D**

SimCLR’s most important pair is random resized crop plus color distortion. This pipeline has neither an effective crop nor color jitter, so even with two views the contrastive task would be too easy. A fix: RandomCrop(24, 24) followed by Resizing(32, 32), plus RandomContrast, RandomBrightness or hue jitter.

- A: ✗ No.
- B: ✗ Keras RandomCrop does not pad.
- C: ✗ A crop the same size as the image has only one possible position.
- D: ✓ Correct. SimCLR crops a random region, then resizes it back.

**Q255 → B**

Siamese margin loss: L = y·d² + (1 − y)·max(m − d, 0)². SimCLR’s NT-Xent treats every other view in the batch as a negative and needs no labels, which is why it scales to unlabeled data.

- A: ✗ SimCLR never uses labels.
- B: ✓ Correct. This is a classic Siamese network with a Hadsell margin loss.
- C: ✗ Choosing positives from labels is exactly what makes it supervised.
- D: ✗ It uses one negative per anchor, not in-batch negatives.

**Q256 → A**

With y = 1: p² = 0.25. With y = 0: max(1 − p, 0)² = 0.25. Your run sat around 0.24–0.26 with accuracy near 0.5, so it was stuck at this trivial solution. Because sigmoid ∈ (0, 1) and the margin is 1, the negative term can never reach 0. Apply the loss to the distance itself, without the sigmoid head.

- A: ✓ Correct. Both terms equal 0.25, and the mean is 0.25.
- B: ✗ For y = 1 the term is p² = 0.25, which is not 0.
- C: ✗ reduce_mean averages over the batch, and each example has only one of the two terms active.
- D: ✗ No.

**Q257 → B**

A single 1×1 cell means pooling has nothing to average, and ImageNet filters are being applied to tiny, unnaturally scaled inputs (no resnet50.preprocess_input). Combined with only about 262K trainable weights, this explains the flat ~0.5 accuracy. Resizing to 224, or fine-tuning the top stages, would help.

- A: ✗ trainable = False freezes every weight in the base.
- B: ✓ Correct. ResNet50 downsamples by 32, so 32/32 = 1. Dense(128): 2048·128 + 128; Dense(1): 2.
- C: ✗ 7×7 is what a 224×224 input gives.
- D: ✗ The ResNet does run, and the Dense layers do train.

**Q258 → C**

Stride-2 ‘same’ convolutions give ⌈H/2⌉, and stride-2 transposed convolutions give 2H. Symmetric encoder–decoder stacks need H divisible by 2^(number of stages). This is a common source of shape bugs.

- A: ✗ Padding is unrelated to the KL term.
- B: ✗ Keras accepts any size.
- C: ✓ Correct. 28 gives 14→7→4 (ceil), and 4 upsampled three times is 32, which no longer matches 28.
- D: ✗ Fashion-MNIST items are already centered.

**Q259 → C**

Only the ratio matters: 500·Rec + KL ∝ Rec + KL/500. binary_crossentropy with axis=(1, 2, 3) averages over 1,024 pixels, so ×500 roughly restores a per-image sum scale. With a larger KL weight, latents fit N(0, I) more tightly but reconstructions blur (the β-VAE trade-off).

- A: ✗ β only appears in the loss.
- B: ✗ The KL term’s relative weight shrinks.
- C: ✓ Correct.
- D: ✗ Adam normalizes per parameter but cannot undo the relative weighting between two terms that share parameters.

**Q260 → B**

z = μ + σ ⊙ ε with ε ~ N(0, I). exp(0.5·log σ²) = σ, which is positive for any real network output. The gradient flows to z_mean and z_log_var, while ε is treated as a constant input.

- A: ✗ exp(log σ²) would be the variance. The 0.5 takes the square root.
- B: ✓ Correct.
- C: ✗ Unrelated.
- D: ✗ Sampling does not change the KL formula.

**Q261 → A, B, C**

These bugs are about tooling, not the model, but they are typical exam-style “spot the bug” items: metric-name mismatches, quantile functions at 0 and 1, and the probability-integral transform (if Z ~ N(0, 1) then Φ(Z) ~ U(0, 1)).

- A: ✓ Correct. Use np.linspace(0.01, 0.99, 15) instead.
- B: ✓ Correct. That is why the p-value plot was used.
- C: ✓ Correct. Keras warns that the monitored metric is unavailable and skips saving.
- D: ✗ BCE works for [0, 1] targets, including the zero padding.

**Q262 → C**

token_type_ids is 0 for [CLS] A [SEP] and 1 for B [SEP], so .index(1) = 8. Each layer’s attention tensor has shape (batch = 1, heads = 12, 15, 15).

- A: ✗ That counts only the words.
- B: ✗ This forgets the [CLS] and one [SEP], or the segment boundary.
- C: ✓ Correct. [CLS] + 6 + [SEP] occupy indices 0–7; segment B starts at 8.
- D: ✗ BERT adds a [SEP] after each segment.

**Q263 → D**

Stacking gives (layers = 12, batch = 1, heads = 12, query = 15, key = 15), and [:, 0] drops the batch axis. So next_tok(L, h) = mean_i A[L, h, i, i+1] measures how much each token looks at the next one.

- A: ✗ No averaging is done.
- B: ✗ The head axis is missing, and the query/key order is reversed.
- C: ✗ Attention tensors hold weights, not value vectors.
- D: ✓ Correct. Rows are queries and each row sums to 1.

**Q264 → B**

The mirror pattern, your layer 3 head 5 previous-token head (0.61), is allowed in both models. Previous-token heads are a known building block of induction heads in GPT-style models.

- A: ✗ Learned positions can still support offset patterns. Previous-token heads are common in GPT-2.
- B: ✓ Correct. BERT has no causal mask, so it can look ahead.
- C: ✗ GPT-2 small has 12 heads per layer.
- D: ✗ Depth is not the reason.

**Q265 → C**

Because softmax weights must sum to 1, a head that is inactive for a given token needs a default target. Studies show that zeroing attention to [SEP] in these layers barely changes outputs. Your layer 4, head 3 finding (first “cat” → second “cat” at 0.86) is the opposite case: a head doing real cross-sentence matching.

- A: ✗ This is not the accepted explanation.
- B: ✗ The pattern is real and well documented (Clark et al., 2019).
- C: ✓ Correct. The weights must sum to 1, so they have to land somewhere.
- D: ✗ [SEP] is a fixed delimiter with no sentence-specific meaning.

