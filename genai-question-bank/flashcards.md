# SEAS 8525 Flashcards

132 cards. Cover the right column and test yourself.

## Class 1 · Introduction to Generative AI

| Prompt | Answer |
|---|---|
| Discriminative vs generative model: what does each estimate? | Discriminative: p(y \| x), a label given an input (logistic regression, CRFs, decision trees). Generative: p(x), or p(x \| y) when conditional. Only a generative model can sample new observations. |
| Why must a generative model be probabilistic? | It needs a random component to produce varied outputs. A fixed calculation, such as averaging pixels, always gives the same result. |
| Three desirable properties of p_model | Accuracy (high p_model ⇒ looks real), Generation (easy to sample), Representation (high-level features are interpretable). |
| Parametric model | A family of densities p_θ(x) described by a finite number of parameters θ. Example: uniform boxes on the map, with 4 parameters (two corners). |
| Likelihood L(θ \| X) for i.i.d. data | ∏ p_θ(x_i). It is 0 if any observed point has density 0 under the model. |
| Why use the log-likelihood? | A product of many terms in (0, 1) underflows. The log turns it into a sum with the same maximizer. |
| Generative modeling as MLE | Find θ (network weights) that maximize the likelihood of the data, i.e., minimize the negative log-likelihood. |
| Taxonomy: tractable explicit density | Autoregressive models (order features, generate sequentially) and normalizing flows (invertible transforms of a simple distribution). |
| Taxonomy: approximate explicit density | VAEs (variational bound), energy-based models (Markov-chain sampling), diffusion models (learned gradual denoising). |
| Taxonomy: implicit density | A stochastic process that generates data directly with no density estimate. GANs are the main example. |
| Why is generative modeling hard? (4 reasons) | High-dimensional space; sparse observations; creative generalization (novel but plausible); explicit density is intractable. |
| Representation learning: core idea | Encode high-dimensional data into a low-dimensional latent space and learn a mapping back to the data domain. Example: biscuit tins described by height and width. |
| Sample space vs true distribution (map example) | The sample space is every (lat, long) point. NYC is in p_data. A point at sea is in the sample space but not in p_data. |
| Generative AI project life cycle (6 stages) | Identify use case → Experiment & select → Adapt & augment (fine-tune, align) → Evaluate → Deploy & integrate → Monitor. |
| Shared ethics principles (military and healthcare) | Traceability, Reliability, Lawfulness, Accountability, Governability, Equity. |
| DDIB (Dual Diffusion Implicit Bridges) | Image-to-image translation: run the source diffusion ODE forward to a shared latent, then run the target ODE in reverse. Needs no paired data. |

## Class 2 · Deep Learning (Vision ↔ NLP)

| Prompt | Answer |
|---|---|
| Conv layer parameter formula | (k_h · k_w · C_in + 1) · filters. It does not depend on the input’s height or width. |
| Dense layer parameter formula | inputs · outputs + outputs (biases). Flatten and pooling layers have 0 parameters. |
| Parameter total: Conv(4×4, 3→10) → Conv(3×3, 10→20) → Flatten(1,280) → Dense(10) | Conv1 490 + Conv2 1,820 + Flatten 0 + Dense 12,810 = 15,120. |
| CIFAR-10 | 60,000 32×32 RGB images, 10 classes, 6,000 per class. Vanilla NN 50.89%, CNN ≈70%, random 10%. |
| CNN feature hierarchy, layer by layer | Input: pixels → low-level: edges and textures → mid-level: parts (eyes, teeth) → high-level: concepts (“smiling”). |
| padding='valid' vs 'same' | valid: no padding, so the output shrinks. same: zero padding keeps the size (stride 1); stride 2 halves it. |
| AlexNet key facts | ReLU everywhere; 3×3 max pooling with stride 2; 3 fully connected layers in the head; biases initialized slightly positive. |
| Residual (skip) connection | f(x) = C(x) + x, so C learns the residual f(x) − x. Identity is easy (C = 0), gradients flow, and the loss landscape is smoother. |
| Degradation problem | Deeper plain networks have higher training error. It is an optimization problem, not overfitting, and residual learning fixes it. |
| DenseNet | Convolutions output 32 channels that are concatenated; 1×1 transition blocks halve the channels; BN + ReLU. |
| MobileNetV2 | Repeated inverted residual bottlenecks with depthwise convolutions, for mobile efficiency. |
| Transfer learning workflow | Load pretrained model → remove head → add small head → freeze feature extractor → train the new layers only. |
| Fine-tuning vs transfer learning | Fine-tuning updates more or all weights (needs more data and compute, adapts better). It is a specialized type of transfer learning. |
| Learning-rate paradox in fine-tuning | Too high: catastrophic forgetting. Too low: very slow convergence. Fixes: LR ramp-up, differential LRs, low LR for early layers. |
| Precision, recall, F1 | Precision: accuracy of positive predictions. Recall: fraction of a class found. F1 = 2PR/(P + R), the harmonic mean. |
| GLO (Generative Latent Optimization) | Tests (A1) convnet inductive bias vs (A2) adversarial training. Jointly optimizes the generator and per-image latents, with no discriminator. GAN-like on CelebA, MNIST, SVHN; worse on LSUN. |
| GAN saddle point | A minimax equilibrium: a minimum for one player and a maximum for the other. Training is sensitive to initialization, architecture and hyperparameters. |
| CPU vs GPU | CPU: low-latency serial work. GPU: high-throughput parallel arithmetic (many ALUs, caches hide memory latency). |

## SimCLR paper (Chen et al., 2020)

| Prompt | Answer |
|---|---|
| SimCLR’s 4 components | Stochastic augmentation (2 views) → base encoder f (ResNet → h) → projection head g (MLP → z) → NT-Xent loss. |
| NT-Xent loss | ℓ_ij = −log [exp(sim(z_i, z_j)/τ) / Σ_{k≠i} exp(sim(z_i, z_k)/τ)], where sim is cosine similarity. Normalized, temperature-scaled cross entropy. |
| Negatives per positive pair | 2(N − 1), the other augmented views in the batch. N = 8192 gives 16,382. No memory bank is used. |
| Most important augmentation pair | Random crop + color distortion. Without color distortion, color histograms are a shortcut. |
| Projection head findings | Nonlinear > linear (+3%) > none (>10%). Use h (before g), not z, downstream, because g discards information such as color and rotation. |
| Why global BN? | Positive pairs sit on the same device, so per-device BN statistics leak a shortcut. Aggregate BN statistics over all devices. |
| Default training setup | ResNet-50, batch 4096, 100 epochs, LARS with LR 4.8 (= 0.3 × B/256), weight decay 1e-6, 10-epoch warmup + cosine decay, 128-d z. |
| Temperature finding | ℓ2 normalization + τ ≈ 0.1 works best. Without normalization, contrastive accuracy rises but linear evaluation falls. |
| Headline results | Linear eval: R50 69.3%, R50(4×) 76.5% top-1 (= supervised R50). 1% labels: 75.5% (R50), 85.8% (4×) top-5. |
| Linear evaluation protocol | Train a linear classifier on the frozen encoder. Its test accuracy is a proxy for representation quality. |
| Batch size and epochs | Larger batches help most for short training. Contrastive learning benefits more than supervised from longer training (up to 1,000 epochs) and bigger models. |

## Class 3 · Autoencoders & VAEs

| Prompt | Answer |
|---|---|
| Latent variable model | Pr(x) = ∫ Pr(x\|z) Pr(z) dz, a likelihood times a prior, marginalized over the latent z. |
| Mixture of Gaussians as an LVM | Discrete z with a categorical prior λ_n; Pr(x\|z=n) = N(μ_n, σ_n²); Pr(x) = Σ λ_n N(x; μ_n, σ_n²). |
| Nonlinear LVM | Prior N(0, I); likelihood N(f[z, φ], σ²I). An infinite mixture of spherical Gaussians. |
| ELBO | A lower bound on log Pr(x\|φ) = E_q[log Pr(x\|z)] − KL(q(z\|x) ‖ Pr(z)). Tight when q equals the true posterior. |
| KL divergence properties | ≥ 0, and = 0 only if identical; asymmetric; infinite if p > 0 where q = 0. It is the information lost when q represents p. |
| Closed-form KL to N(0, I) | −0.5 · Σ(1 + log σ² − μ² − σ²). |
| Reparameterization trick | z = μ + σ ⊙ ε with ε ~ N(0, I) and σ = exp(0.5 · log_var). Sampling becomes differentiable. |
| Why output log variance? | The network output can be any real number; exp(log_var) is always positive. |
| AE vs VAE encoder | AE maps to a single point, giving a gappy latent space. VAE maps to a Gaussian around a point, giving a continuous latent space; KL keeps it centered. |
| Problems with the plain AE latent space | Variable density, asymmetry about (0, 0), large gaps, so random points decode badly. |
| VAE loss | Reconstruction loss + β · KL(q(z\|x) ‖ N(0, I)). |
| CelebA VAE changes | 3 channels; latent 2 → 200; β = 2,000; batch norm after each conv. |
| Latent arithmetic and morphing | Smile vector = mean(smiling z) − mean(non-smiling z); z_new = z + α·v. Morph: z = z_A(1−α) + z_B α. |
| Ancestral sampling | Sample in the order of the factorization: root first, then each conditional (z ~ prior, then x ~ Pr(x\|z)). |
| Conv2DTranspose | Upsamples: smaller spatial input with more channels → larger output with fewer channels. |
| Fashion-MNIST AE encoder shapes | 32×32×1 → (3 stride-2 convs: 32, 64, 128) → 4×4×128 = 2,048 → Dense(2). Loss: binary cross-entropy. |
| ECMVAE key ideas | Shared c + specific s_a, s_v latents; orthogonality constraint; mutual-information maximization; JS divergence; frozen VGGish audio; TPAVI decoder. |
| AVSBench | 5,356 videos. S4 = single source, MS3 = multiple sources. Metrics: mIoU and F-score. ECMVAE: +3.00 / +3.84 mIoU. |

## Class 4 · Transformers

| Prompt | Answer |
|---|---|
| Scaled dot-product attention | softmax(QKᵀ / √d_k) V. |
| Why scale by √d_k? | Dot products grow with d_k, which saturates the softmax and gives tiny gradients. |
| Q, K, V intuition | Query = the current task; Key = what each token can help with; Value = each token’s content. A soft key-value lookup. |
| Where are the learnable weights in attention? | W_Q, W_K, W_V (and W_O for multi-head). The attention arithmetic itself has no parameters. |
| Additive vs dot-product attention | Similar complexity; dot-product is faster and memory-efficient on GPUs. Unscaled dot-product loses at large d_k. |
| Sinusoidal positional encoding | PE(pos, 2i) = sin(pos/10000^{2i/d}), PE(pos, 2i+1) = cos(·). PE_{pos+k} is linear in PE_pos. |
| Multi-head attention | Separate Q/K/V projections per head → concatenate → W_O. Heads attend to different subspaces and relations. |
| Causal mask | Set scores of future positions to −∞ before softmax. Keeps generation autoregressive while training stays parallel. |
| Cross-attention | Q from the decoder; K and V from the encoder output. |
| Encoder-only / decoder-only / encoder–decoder | BERT (bidirectional, classification, NER) / GPT (left context, generation) / T5, BART (seq2seq: translation, summarization). |
| BERT pretraining tasks | MLM (predict masked tokens from both sides) + NSP (50% IsNext / 50% NotNext). |
| BERT sizes | Base: L12, H768, A12, 110M. Large: L24, H1024, A16, 340M. Data: BooksCorpus 800M + Wikipedia 2,500M words. |
| BERT input embedding | Token + segment + position embeddings. |
| T5 | Text-to-text: every task is text in, text out, using one encoder–decoder. |
| Layer norm | Per-sample mean 0 and variance 1 across features, then learnable γ and β. Independent of the batch, unlike batch norm. |
| T-DMCA | Local attention (blocks) + memory-compressed attention (strided conv, kernel 3, stride 3, on K and V) for long sequences. |
| Causal mediation analysis | IV = input, DV = output, mediators = neurons, layers, heads. Direct effect: vary input, fix mediator. Indirect effect: the effect through the mediator. |
| FFN layers as key-value memories (Geva) | Keys detect patterns (shallow in lower layers, semantic in upper layers); values are distributions over the vocabulary. |
| MEMIT | Mass-edits thousands of facts in critical mid-layer MLPs found by causal tracing. Criteria: effectiveness, generalization, specificity, fluency. Tested on GPT-J and GPT-NeoX. |

## Class 5 · Autoregressive Models

| Prompt | Answer |
|---|---|
| Autoregressive factorization | p(x) = ∏ p(x_t \| x_<t). Exact, tractable likelihood; sequential generation. |
| Positional embedding options | Additive (same dimension), concatenation (dimension grows), learned (trainable, as in ViT). Large magnitudes destroy semantics. |
| RNN weights U, W, V | U: input→hidden, W: hidden→hidden, V: hidden→output. Shared across time. |
| BPTT steps | Unroll → forward → loss (each step or final) → backward → sum gradients over time (shared weights) → update. |
| Why RNN gradients vanish or explode | Products of many Jacobians over time. Vanishing is common; exploding is rare but damaging. |
| LSTM gates | Forget (self-loop weight of the cell), input (write), output (expose). All sigmoid. The linear cell self-loop carries memory. |
| GRU gates | Update gate (how much old state to keep) + reset gate (how much past state feeds the candidate). Reset ≈ 0 ignores the past. |
| Luong global vs local attention | Global: all source states, blurrier alignment, dot scoring best. Local: predicted position p_t plus a window, sharper alignment, general scoring best for predictive. |
| Luong results | +5.0 BLEU over non-attentional systems. The ensemble reached 25.9 BLEU on WMT’15 En→De (+1.0 over previous best). |
| PixelCNN masks | Type A (first layer): excludes the center and future pixels. Type B (later layers): includes the center. Raster-scan order. |
| PixelCNN building blocks | Masked convolutions + residual blocks; outputs a distribution per pixel. |

## Class 6 · Multimodal LLMs

| Prompt | Answer |
|---|---|
| BPE | Start from characters; repeatedly merge the most frequent adjacent pair into a new symbol, so subwords emerge. |
| GPT-2 adaptive input and softmax | Bigger embeddings for frequent words; vocabulary clustered by frequency (e.g., 100 / 900 / 9,000) to cheapen the softmax. |
| GPT-3 improvements | 175B parameters (June 2020); sparse attention; multi-head refinements; pipeline efficiency. |
| ViT recipe | 16×16 patches → linear projection → + learnable 1-D positions → [class] token → pre-LN Transformer (MSA + GELU MLP). |
| ViT inductive bias | Lacks CNN locality and translation equivariance, so it needs large-scale data. |
| ViT positional embedding finding | 1-D, 2-D and relative all perform similarly; 1-D learns 2-D structure. |
| Mean attention distance | Grows with depth. Early layers mix local and global heads; late layers are global. |
| Quadrangle attention (“QFormer”) | Learned projective transform turns square windows into quadrangles; decomposed into scale, shear, rotation, translation, projection. Not BLIP-2’s Q-Former. |
| CLIP training | Image and text encoders; symmetric cross-entropy over cosine similarities. WIT: 400M pairs, 500K queries, ≤20K per query. |
| CLIP zero-shot | Encode class names as text and pick the most similar to the image. Matches 4-shot logistic regression; up to 75% smaller robustness gap. |
| CLIP limitations | Specialized domains (PatchCamelyon), social bias, surveillance misuse. Fine-tuning on ImageNet reduces robustness. |
| DALL·E 2 pipeline | CLIP text encoder → prior (text embedding → image embedding) → decoder (image from embedding + text). |
| BLIP | MED (multimodal mixture of encoder–decoder) + CapFilt (synthetic captions + noise filtering). |
| BLIP-2 | Frozen image encoder + frozen LLM. The Q-Former learns vision-language representations, then a projection feeds a soft visual prompt to the LLM. |
| Pic2Word | Zero-shot composed image retrieval. A mapping network turns a frozen CLIP image embedding into a pseudo-word token, trained on unlabeled images. |
| ScreenAI | PaLI + Pix2Struct patching; 670M / 2B / 5B parameters; auto-annotated screen schema + LLM-generated tasks; SOTA on UI and infographic tasks. |
| Flamingo architecture | Frozen NFNet-F6 → Perceiver Resampler (64 tokens) → frozen LM interleaved with tanh-gated cross-attention (α = 0 at init). |
| Flamingo image-causal masking | Each text token cross-attends only to the image just before it. Trained with 5 images; evaluated with up to 32. |
| Flamingo limitations | Inherits LM hallucinations; classification behind contrastive models; in-context learning is sensitive to demonstrations. |

## Class 7 · Diffusion Models

| Prompt | Answer |
|---|---|
| Diffusion model in one line | A fixed forward process gradually adds Gaussian noise; a learned reverse process denoises step by step. Latents have the same size as the data. |
| Forward step | z_t = √(1−β_t) z_{t−1} + √β_t ε_t. A Markov chain that keeps unit variance. |
| Diffusion kernel | q(z_t \| x) = N(√ᾱ_t x, (1−ᾱ_t) I), ᾱ_t = ∏(1−β_s). Jump to any t in one step. |
| Marginal q(z_t) | The distribution of z_t over all starting data and all paths. It blurs toward N(0, I) as t grows. |
| q(z_{t−1} \| z_t) vs q(z_{t−1} \| z_t, x) | The first is intractable (needs the marginal). Conditioning on x gives a closed-form Gaussian whose mean blends z_t and x. |
| Decoder (reverse) model | Pr(z_{t−1} \| z_t) = N(f_t[z_t, φ_t], σ_t² I), with fixed variances. Valid when β_t is small and T is large. |
| Training objective | Maximize the ELBO (via Jensen’s inequality). In practice, predict the added noise ε with a least-squares (or MAE) loss. |
| Noise schedules | DDPM: β linear from 1e-4 to 0.02 over T = 1,000. A later cosine schedule works better. |
| Diffusion U-Net | Down and up paths with concatenated skips; residual blocks + self-attention; one network for all t via a sinusoidal time embedding. |
| DDIM | σ_t = 0 gives a deterministic sampler: same noise → same image. Allows few steps (e.g., 20 instead of 1,000). |
| DDIM step | Estimate x̂₀ from ε̂, then re-noise it to level t−1 using the signal and noise rates. |
| Spherical interpolation of noise | sin/cos weights keep the variance at 1, so every interpolant is valid N(0, I) input. |
| Classifier vs classifier-free guidance | Classifier: add the gradient of p(c\|z). Classifier-free: class embedding in the U-Net, trained conditionally and unconditionally; trades quality for diversity. |
| Cascaded text-to-image | 64×64 → 256×256 → 1024×1024, each stage conditioned on the text embedding and the lower-resolution image. |
| Sora | Video → compressed latent → spacetime patches → diffusion transformer. Native sizes; GPT-expanded prompts; emergent 3D consistency. Weak at physics. |

## Cross-topic synthesis

| Prompt | Answer |
|---|---|
| Exact likelihood? | Autoregressive and flows: exact. VAE and diffusion: bound. GAN: none. |
| Sampling cost by family | VAE and GAN: 1 pass. Diffusion: T steps (≈20 with DDIM). Autoregressive: 1 pass per element. |
| Where contrastive losses appear | SimCLR (views), CLIP (image–text), Pic2Word (pseudo token), Flamingo’s vision encoder pretraining. |
| Where masking appears | GPT causal mask, PixelCNN masked convolutions, BERT MLM inputs, Flamingo image-causal cross-attention. |
| Frozen backbone + small trainable bridge | BLIP-2 (Q-Former), Flamingo (resampler + gated cross-attention), Pic2Word (mapping network), transfer learning. |
