# SEAS 8525 Generative AI Question Bank

178 questions from Classes 1–7 and the SimCLR paper.

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

**Q2.** ☐ *Select all that apply.* According to the lecture, which properties are required for a model to count as a true generative model? Select all that apply.

- ☐ **A.** It must be a fixed computation, such as averaging the pixel values of the training images, so the output is reproducible
- ☐ **B.** It must be probabilistic, with a random component, so it can produce varied outputs
- ☐ **C.** It must use labeled data so that each generated sample has a known class
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

**Q8.** ○ *Single answer.* Representation learning is motivated in the lecture with the “describe yourself in ~10 features” analogy and the biscuit-tin example. What is the core idea?

- ○ **A.** Increase the dimensionality of the data so that the classes become linearly separable for a downstream discriminator
- ○ **B.** Hand-code the important features (e.g., height, width) so the machine does not need to learn them
- ○ **C.** Encode data into a low-dimensional latent space and learn a mapping from latent points back to data
- ○ **D.** Store every training image in a lookup table and retrieve the nearest one at generation time

**Q9.** ☐ *Select all that apply.* Which reasons does the lecture give for why generative modeling of high-dimensional data is hard? Select all that apply.

- ☐ **A.** Training data covers only a sparse subset of the possible observations
- ☐ **B.** The true distribution lives in an exponentially high-dimensional space
- ☐ **C.** Explicitly modeling the full dimensionality, i.e., computing p_θ(x) directly, is generally intractable
- ☐ **D.** The sample space is discrete, so densities cannot be defined
- ☐ **E.** Discriminative models already solve the problem, so there is little demand for better generative models from industry or research

**Q10.** ○ *Single answer.* The lecture lists three desirable properties of a generative model p_model. Which set is correct?

- ○ **A.** Convexity, sparsity, and calibration
- ○ **B.** Determinism, reproducibility, and explainability, since outputs should be identical across runs
- ○ **C.** Accuracy, generation, and representation
- ○ **D.** Speed, memory efficiency, and differentiability

**Q11.** ○ *Single answer.* Which ordering of the Generative AI project life cycle matches the lecture?

- ○ **A.** Identify use case → Experiment & select → Adapt & augment → Evaluate → Deploy → Monitor
- ○ **B.** Collect data → Train a new model from scratch → Evaluate on a held-out set → Deploy
- ○ **C.** Experiment & select → Identify use case → Deploy & integrate → Adapt & augment → Monitor → Evaluate
- ○ **D.** Identify use case → Deploy the base model → Fine-tune on production logs → Monitor drift

**Q12.** ☐ *Select all that apply.* The healthcare and military ethics comparison (Oniani et al., 2023) identified shared core principles. Which of the following were listed as shared principles? Select all that apply.

- ☐ **A.** Governability
- ☐ **B.** Equity
- ☐ **C.** Maximum autonomy without human oversight
- ☐ **D.** Profitability
- ☐ **E.** Traceability

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

**Q21.** ○ *Single answer.* Why did industry historically favor discriminative models over generative ones, according to the lecture?

- ○ **A.** Generative models cannot run on GPUs
- ○ **B.** Generative models were illegal to deploy
- ○ **C.** They were easier to apply to practical tasks, e.g., doctors wanted diagnoses, not new images
- ○ **D.** Discriminative models need no training data, while every generative model needs millions of labeled examples


### Answer key — Class 1 · Introduction to Generative AI

**Q1 → A**

Discriminative (conditional) models such as logistic regression, CRFs and decision trees model p(y|x) directly and learn decision boundaries. Generative models model p(x), or p(x|y) when conditional, and sampling from that distribution is what produces new observations. Foster’s point is that even a perfect Van Gogh classifier only outputs probabilities against existing images.

- A: ✓ Correct. A discriminative model only learns the conditional p(y|x); it never models how x itself is distributed, so it cannot sample new x.
- B: ✗ Sampling from p(y|x) yields labels, not images. Temperature does not change what space you sample in.
- C: ✗ Bayes’ rule needs p(x) as well; a classifier alone does not give you p(x|y). The lecture’s “word of caution”: even a perfect discriminator has no idea how to create a painting.
- D: ✗ Training on images does not make a model generative; what matters is whether it models p(x) (or p(x|y)).

**Q2 → B, D**

The slides list the goals of generative modeling: novel observations, a stochastic component, the ability to handle combinatorially many arrangements, and non-fixed logic. A generative model must sample variations, so it has to be probabilistic.

- A: ✗ This is the textbook example of what is not generative. Averaging pixels is deterministic and yields one output.
- B: ✓ Correct. The “generative mandate”: deterministic calculations always return the same output.
- C: ✗ Generative modeling is usually unsupervised; labels are optional and only needed for conditional generation.
- D: ✓ Correct. The goal is new observations that mimic the training-data patterns, not copies of them.

**Q3 → D**

A parametric model is a family of densities p_θ(x) described by a finite number of parameters. For the box family the density is 0 outside the box and constant inside it, with the constant chosen so that the density integrates to 1 over the sample space.

- A: ✗ A center alone does not fix the box’s width and height.
- B: ✗ That describes squares only. The orange box can be any rectangle.
- C: ✗ The density is defined everywhere, but it is parameterized by a finite set of numbers. That finiteness is the definition of a parametric model.
- D: ✓ Correct. Four numbers uniquely define each box, and therefore each density in the family.

**Q4 → C**

For independent observations L(θ|X) = ∏ p_θ(x_i). The lecture’s example: a box covering only the left half has likelihood 0 because it could not possibly have generated points observed on the right half.

- A: ✗ The likelihood of i.i.d. data is a product, not an average.
- B: ✗ Likelihood is not the fraction of area covered. It depends on the density at the observed points.
- C: ✓ Correct. One zero factor in ∏ p_θ(x_i) makes the whole product zero.
- D: ✗ log(0) = −∞ is a perfectly meaningful log-likelihood. The likelihood itself is simply 0.

**Q5 → B**

MLE finds θ̂ = argmax_θ ℓ(θ|X). Equivalently, generative modeling minimizes the negative log-likelihood, where θ are the network weights. The log is used because multiplying thousands of small terms is numerically unstable.

- A: ✗ Neural-network log-likelihoods are generally non-convex. The log does not make them convex.
- B: ✓ Correct. This is the computational reason the slides give, and sums are also easier to differentiate.
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

The conditional generative model estimates p(x|y). The slide calls this “guided generation”: condition on a label to choose what kind of observation is sampled.

- A: ✗ The class prior tells you how common apples are. It cannot generate an apple.
- B: ✗ That is the discriminative objective.
- C: ✗ Conditioning is a standard way to guide generation (e.g., classifier-free guidance in diffusion).
- D: ✓ Correct. Conditioning on y = apple steers sampling toward apple images.

**Q8 → C**

Rather than modeling pixels directly, we model a compact latent space where each point summarizes an observation. Sampling a new latent point and decoding it produces new data, including tins not in the training set. Editing the latent point (e.g., increasing height) makes targeted, intuitive changes.

- A: ✗ Kernel-style lifting is a different idea. Representation learning here compresses.
- B: ✗ The slides stress that a machine must identify latent features and the mapping itself, which is nontrivial.
- C: ✓ Correct. Height and width form a 2-D latent space for tins, and a learned decoder maps (h, w) back to pixels.
- D: ✗ That is memorization, which cannot produce novel tins.

**Q9 → A, B, C**

The four slide bullets are: high-dimensional space, sparse observations, the need for creative generalization (novelty balanced with plausibility), and intractable explicit modeling.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✓ Correct. Each model family tackles this intractability differently.
- D: ✗ Images are usually treated as continuous. Densities are well defined.
- E: ✗ The slides argue the opposite: generative modeling is essential for the next leap in AI and is now offered as a cloud service.

**Q10 → C**

Accuracy: if p_model is high for a generated observation it should look like it came from p_data, and if low it should not. Generation: it should be easy to sample a new observation. Representation: it should be possible to understand how high-level features are represented by p_model.

- A: ✗ None of these are the listed properties.
- B: ✗ Determinism contradicts the generative mandate.
- C: ✓ Correct. High p_model should mean the sample looks real; sampling should be easy; features should be interpretable.
- D: ✗ These are engineering concerns, not the three properties listed.

**Q11 → A**

Lecture details: start small (e.g., 7B models) in a playground such as SageMaker JumpStart; adapt by fine-tuning and aligning to helpful, honest and harmless values; establish metrics; optimize for inference before deployment on endpoints; then monitor with tools like CloudWatch and CloudTrail.

- A: ✓ Correct. Six stages, starting from a single well-defined use case.
- B: ✗ The lifecycle explicitly starts from existing foundation models instead of training from scratch.
- C: ✗ Use-case identification comes first, and evaluation precedes deployment.
- D: ✗ Missing stages, and fine-tuning happens before deployment.

**Q12 → A, B, E**

Shared core principles: Traceability, Reliability, Lawfulness, Accountability, Governability, Equity. Military-specific concerns included adversarial AI, human–machine teaming and the arms race. Healthcare concerns included empathy, autonomy and privacy.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✗ Autonomy appears as a healthcare concern, not as an unconstrained principle. Governability implies human oversight.
- D: ✗ Not an ethical principle on the slide.
- E: ✓ Correct.

**Q13 → A**

Given x(s), the source ODE runs forward to the latent x(l); the target, reverse ODE then constructs x(t). Because each diffusion model is trained independently, the method can use pre-trained conditional diffusion models.

- A: ✓ Correct. Two diffusion models share the latent space reached by their deterministic ODEs.
- B: ✗ That describes CycleGAN-style training, not DDIBs.
- C: ✗ No VAE is involved.
- D: ✗ DDIBs do not need paired data or adversarial training.

**Q14 → B**

The slides contrast supervised (labeled data, direct feedback, predict outcomes), unsupervised (no labels, no feedback, find structure) and RL (decision process, reward system, learn a series of actions).

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

A density describes relative likelihood for a continuous variable; only integrals over regions are probabilities. The joint wind speed and direction example on the slide is a 2-D density.

- A: ✗ The uniform box density is discontinuous at its edges yet valid.
- B: ✗ Densities can exceed 1. A narrow Gaussian peaks well above 1.
- C: ✓ Correct.
- D: ✗ Many valid densities are skewed.

**Q20 → B, C, D**

Clustering is used for market segmentation and image compression. Dimensionality reduction helps visualization, noise reduction and computational efficiency. Prince’s taxonomy places generative, probabilistic and latent-variable models under unsupervised learning.

- A: ✗ That is supervised, discriminative learning.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct. It sits in the taxonomy under unsupervised learning.

**Q21 → C**

The shift came as cloud services began offering generative modeling via APIs: automated content generation, visual product rendering and brand-tailored advertising.

- A: ✗ They run on GPUs.
- B: ✗ Not a reason given.
- C: ✓ Correct.
- D: ✗ Both need data. Generative models are usually unsupervised.


---

## Class 2 · Deep Learning (Vision ↔ NLP)

**Q22.** ○ *Single answer.* A Conv2D layer has 5 filters of size 4×4 applied to a 3-channel input. Ignoring biases, how many learnable weights does it have?

- ○ **A.** (4 × 4 × 3 + 1) × 5 = 245, which is the count without biases
- ○ **B.** 4 × 4 × 3 × 5 = 240
- ○ **C.** 32 × 32 × 3 × 5, because weights scale with the image size
- ○ **D.** 4 × 4 × 5 = 80

**Q23.** ○ *Single answer.* Compute the total learnable parameters for: Conv(4×4, 3→10) → Conv(3×3, 10→20) → Flatten (1,280 units) → Dense(10).

- ○ **A.** 15,120
- ○ **B.** 16,400, because Flatten adds one weight for each of its 1,280 output units and then one bias
- ○ **C.** 12,810
- ○ **D.** 14,630

**Q24.** ☐ *Select all that apply.* Which statements about the AlexNet design as described in the lecture are correct? Select all that apply.

- ☐ **A.** Every convolutional layer uses sigmoid activations because ReLU had not yet been introduced in 2012
- ☐ **B.** Max-pooling layers downsample height and width; AlexNet uses 3×3 max-pooling with stride 2
- ☐ **C.** Convolutional layers change the depth (number of channels) of the data
- ☐ **D.** The classification head is a single linear layer with no bias
- ☐ **E.** With ReLU, biases start slightly positive so every layer begins with nonzero output and gradient

**Q25.** ○ *Single answer.* A residual (skip) connection computes f(x) = C(x) + x. What does the convolutional path C learn, and why does this help very deep networks?

- ○ **A.** C learns the residual f(x) − x; identity is just C = 0, and gradients flow through the skip
- ○ **B.** C learns the full mapping f(x); the skip only adds regularization noise
- ○ **C.** C learns to output zero always, so the network reduces to a shallow linear model
- ○ **D.** C learns x − f(x), and the skip connection performs channel-wise concatenation of the input and output rather than an addition

**Q26.** ○ *Single answer.* Which architecture is built from repeated inverted residual bottlenecks with depthwise convolutions?

- ○ **A.** DenseNet
- ○ **B.** ResNet-50
- ○ **C.** MobileNetV2
- ○ **D.** AlexNet, in its original two-GPU form with grouped convolutions

**Q27.** ☐ *Select all that apply.* Which statements correctly distinguish transfer learning from fine-tuning, as presented? Select all that apply.

- ☐ **A.** Fine-tuning is considered a specialized type of transfer learning
- ☐ **B.** Transfer learning requires more labeled data than fine-tuning because it trains all layers from scratch
- ☐ **C.** Transfer learning typically freezes the pretrained layers and trains only a new head
- ☐ **D.** Fine-tuning updates weights across the model and needs more data and compute

**Q28.** ○ *Single answer.* When fine-tuning, the learning rate is set too high. What failure mode does the lecture name?

- ○ **A.** Posterior collapse, where the pretrained layers stop sending any signal to the new classification head
- ○ **B.** Exposure bias, where the model has never seen its own predictions as inputs during training
- ○ **C.** Catastrophic forgetting, which destroys the valuable pretrained knowledge
- ○ **D.** Mode collapse, where the network maps many different inputs to the same few outputs

**Q29.** ○ *Single answer.* On CIFAR-10, the vanilla dense network reached 50.89% test accuracy and the CNN about 70%. What is the main reason for the gap?

- ○ **A.** CNNs have far more learnable parameters than dense networks, so they can memorize more of the 50,000 training images
- ○ **B.** CIFAR-10 has only 10 classes, which favors convolution
- ○ **C.** Dense networks cannot use ReLU activations, so they are stuck with saturating sigmoids that slow learning
- ○ **D.** Local, weight-shared filters exploit spatial structure; a flattened dense net ignores pixel adjacency

**Q30.** ☐ *Select all that apply.* Generative Latent Optimization (GLO) was used to disentangle the sources of GAN success. Which statements are correct? Select all that apply.

- ☐ **A.** GLO keeps (A1) by using a deep convolutional generator but drops (A2), with no discriminator
- ☐ **B.** GLO shows that the adversarial game, not the convolutional architecture, is the dominant factor behind GAN image quality
- ☐ **C.** GLO outperformed GANs on every dataset it was tested on, including the complex LSUN scenes, while also training faster
- ☐ **D.** GAN success is split into (A1) the convnet inductive bias and (A2) the adversarial protocol
- ☐ **E.** GLO jointly optimizes the generator and each image’s latent vector to minimize reconstruction error

**Q31.** ○ *Single answer.* GAN training is described as seeking a saddle point. What does this mean?

- ○ **A.** A minimum for one player and a maximum for the other: a minimax equilibrium
- ○ **B.** A point where every gradient is zero and the Hessian is positive definite in all directions, i.e., a strict local minimum
- ○ **C.** The point in training at which the learning rate is halved, which stabilizes the two players
- ○ **D.** A point that is a global minimum of a single shared loss function

**Q32.** ○ *Single answer.* Why are GPUs preferred to CPUs for deep learning, according to the lecture?

- ○ **A.** GPUs have no caches, which removes memory latency
- ○ **B.** GPUs are optimized for low-latency serial execution of complex branching code
- ○ **C.** GPUs run at higher clock speeds than any CPU, so each individual operation finishes sooner
- ○ **D.** They maximize throughput on parallel arithmetic such as matrix multiplies

**Q33.** ○ *Single answer.* The F1 score is defined as

- ○ **A.** the arithmetic mean of precision and recall, (P + R) / 2
- ○ **B.** the harmonic mean of precision and recall, 2PR / (P + R)
- ○ **C.** recall divided by precision, so that it equals 1 when the two are balanced
- ○ **D.** the fraction of all predictions that are correct across every class, regardless of class imbalance

**Q34.** ○ *Single answer.* How does the relationship between NLP and vision as described in the lecture differ between the past and today?

- ○ **A.** NLP has always led vision, since CNNs were invented for text
- ○ **B.** NLP once borrowed from vision; today vision borrows from NLP (attention, ViT)
- ○ **C.** Vision abandoned transfer learning, while NLP adopted it from computer vision only after the arrival of large language models
- ○ **D.** Vision and NLP have always developed independently

**Q35.** ☐ *Select all that apply.* Which statements about pooling layers are correct? Select all that apply.

- ☐ **A.** Max pooling increases the number of channels, which is how a CNN grows deeper feature maps over its layers
- ☐ **B.** 2×2 max pooling keeps only the maximum value in each group
- ☐ **C.** Pooling layers have no learnable parameters
- ☐ **D.** Average pooling averages the values in each group

**Q36.** ○ *Single answer.* A Conv2D layer uses kernel size 3×3, 64 input channels and 128 filters, with bias. How many learnable parameters does it have?

- ○ **A.** 73,856
- ○ **B.** 73,728
- ○ **C.** 8,320
- ○ **D.** 1,152, because each filter is 3×3 and is shared across all 128 output channels

**Q37.** ○ *Single answer.* In tf.keras.layers.Conv2D, what does padding='same' do with stride 1?

- ○ **A.** Adds no padding, so the output shrinks
- ○ **B.** Forces all filters to share the same weights
- ○ **C.** Zero-pads the input so the output keeps the same height and width
- ○ **D.** Copies the edge pixels outward so that the convolution can see a mirror image of the border

**Q38.** ☐ *Select all that apply.* Why are pretrained vision models needed, according to the lecture? Select all that apply.

- ☐ **A.** Pretrained models are guaranteed to specialize perfectly to any target domain without further adaptation
- ☐ **B.** Training such large models from scratch on a small dataset is not feasible
- ☐ **C.** They encode visual features learned from huge datasets like ImageNet
- ☐ **D.** Architectures like ResNet, Xception and MobileNet have millions of parameters

**Q39.** ○ *Single answer.* In the transfer-learning workflow, which step comes right after removing the pretrained model’s prediction head?

- ○ **A.** Add a small custom classification head for the new classes
- ○ **B.** Deploy the model
- ○ **C.** Retrain the entire network from random initialization so that ImageNet-specific features are removed
- ○ **D.** Freeze all weights including the new head

**Q40.** ○ *Single answer.* In Foster’s feature hierarchy (units A → D), what does a unit C typically represent?

- ○ **A.** Simple edges and textures
- ○ **B.** Mid-level parts such as eyes or teeth
- ○ **C.** The abstract concept “smiling”, which summarizes the whole face into a single high-level label
- ○ **D.** Raw pixel values for a single color channel

**Q41.** ○ *Single answer.* DenseNet uses 1×1 convolutions in its transition blocks. What do they do?

- ○ **A.** Double the spatial resolution
- ○ **B.** Halve the number of channels
- ○ **C.** Replace the batch normalization layers, which are not used anywhere else in the DenseNet blocks
- ○ **D.** Add skip connections by element-wise addition


### Answer key — Class 2 · Deep Learning (Vision ↔ NLP)

**Q22 → B**

With biases the formula is (k_h × k_w × C_in + 1) × filters. The weight count, 240 here, does not depend on the input’s height or width, which is why convolutions are parameter-efficient.

- A: ✗ 245 is the count with one bias per filter; the question asks to ignore biases.
- B: ✓ Correct. Each filter is 4×4×3 and there are 5 independent filters.
- C: ✗ Convolution shares weights spatially; parameter count is independent of image size.
- D: ✗ This forgets that each filter spans all 3 input channels.

**Q23 → A**

Conv1: (4·4·3 + 1)·10 = 490. Conv2: (3·3·10 + 1)·20 = 1,820. Flatten: 0. Dense: 1,280·10 + 10 = 12,810. Non-parametric layers (Flatten, MaxPool) contain zero learnable parameters.

- A: ✓ Correct. 490 + 1,820 + 0 + 12,810 = 15,120.
- B: ✗ Flatten has zero learnable parameters.
- C: ✗ That is only the dense layer.
- D: ✗ This omits the 490 parameters of the first convolution.

**Q24 → B, C, E**

AlexNet: conv layers change depth, max-pool layers downsample spatially, ReLU everywhere, additive biases in all conv and FC layers, and a three-FC-layer classification head.

- A: ✗ AlexNet popularized ReLU; every conv layer is ReLU-activated.
- B: ✓ Correct. These are overlapping pooling windows.
- C: ✓ Correct.
- D: ✗ The head flattens the final feature map and feeds it through three fully connected layers, all with additive bias.
- E: ✓ Correct. This avoids dead units at initialization.

**Q25 → A**

He et al. (2016): deeper plain networks suffer degradation because solvers struggle to fit identity mappings with stacked nonlinear layers. The residual formulation H(x) = F(x) + x makes identity trivial. Li et al. (2017) show skips turn a chaotic 56-layer loss landscape into a smoother one.

- A: ✓ Correct. This addresses both the degradation problem and vanishing gradients.
- B: ✗ With the skip, C only needs to learn the residual.
- C: ✗ C = 0 is possible but not forced. It is learned only where identity is optimal.
- D: ✗ The sign is wrong, and ResNet skips use element-wise addition. Concatenation is DenseNet and U-Net style.

**Q26 → C**

MobileNetV2 repeats inverted residual bottlenecks: expand → depthwise conv → project, for mobile efficiency. ResNet and DenseNet use ReLU and batch normalization; DenseNet’s 1×1 transitions halve channel count.

- A: ✗ DenseNet concatenates features, uses 32-channel conv outputs and 1×1 transition layers that halve channels.
- B: ✗ ResNet uses standard (not inverted) bottleneck residual blocks.
- C: ✓ Correct. “dw-cnv” in the diagram denotes depthwise convolutions.
- D: ✗ AlexNet predates inverted residual bottlenecks.

**Q27 → A, C, D**

Workflow: load a pretrained model, remove the prediction head, add a small custom head, freeze the feature extractor, and train only the new layers. Fine-tuning goes further, adapting pretrained weights by backpropagation for higher task performance.

- A: ✓ Correct. The slide states this relationship explicitly.
- B: ✗ Backwards: transfer learning needs the least data since most weights are frozen.
- C: ✓ Correct.
- D: ✓ Correct.

**Q28 → C**

Remedies listed: (1) LR ramp-up from a low initial value; (2) differential learning rates per layer; (3) low LR for early (generic) layers and higher LR for later (task-specific) layers.

- A: ✗ A VAE failure mode in which the decoder ignores the latent.
- B: ✗ An autoregressive sequence-model issue, unrelated to fine-tuning learning rates.
- C: ✓ Correct. A too-low LR causes the opposite problem: very slow convergence.
- D: ✗ A GAN failure mode.

**Q29 → D**

CIFAR-10 has 60,000 32×32 RGB images in 10 mutually exclusive classes (6,000 per class). Random guessing gives 10%. CNN filters detect edges, then parts, then concepts, as in Foster’s units A → D.

- A: ✗ CNNs usually have far fewer parameters (15,120 in the lecture example).
- B: ✗ The class count does not favor any architecture.
- C: ✗ They can.
- D: ✓ Correct. The inductive biases of locality and translation equivariance fit images.

**Q30 → A, D, E**

GLO: pair each image with a random vector, train a generator to reconstruct the image from its vector, and optimize both. Competitive results without adversarial training suggest that much of a GAN’s success comes from the convnet prior.

- A: ✓ Correct.
- B: ✗ The finding points the other way: (A1), the convnet inductive bias, is a dominant factor.
- C: ✗ GLO performed worse than GANs on LSUN, though it reproduced GAN-like properties on CelebA, MNIST and SVHN.
- D: ✓ Correct.
- E: ✓ Correct. Each image is paired with a random vector that is then learned.

**Q31 → A**

GAN optimization is min_G max_D V(D, G). It is sensitive to initialization, architecture and hyper-parameters, and the slides call stabilizing it “more art than science.” When the discriminator becomes too accurate, generator gradients vanish (Arjovsky & Bottou, 2017).

- A: ✓ Correct. The generator and discriminator compete.
- B: ✗ That is a strict local minimum, not a saddle.
- C: ✗ Unrelated.
- D: ✗ GANs have two players with opposing objectives, not one shared minimum.

**Q32 → D**

CPU: few powerful cores, low latency, serial. GPU: thousands of ALUs, high throughput, parallel. Training is dominated by matrix multiplies, which are embarrassingly parallel.

- A: ✗ The slide notes GPU caches convert long-latency memory accesses into short-latency ones.
- B: ✗ That describes CPUs.
- C: ✗ Clock speed is not the main advantage. Massive parallelism is.
- D: ✓ Correct.

**Q33 → B**

Precision is the accuracy of positive predictions for a class. Recall is the fraction of a class’s images correctly classified. F1 is their harmonic mean, so it is low if either is low.

- A: ✗ F1 uses the harmonic mean, which penalizes imbalance between the two.
- B: ✓ Correct.
- C: ✗ Not a standard metric.
- D: ✗ That is accuracy.

**Q34 → B**

Progression: vision moved from CNNs to foundation vision models to transfer learning; NLP moved from RNNs to Transformers to LLMs to transfer learning. Attention now appears in vision (ViT), and joint models like VisualBERT combine both.

- A: ✗ CNNs came from vision.
- B: ✓ Correct.
- C: ✗ Both fields use transfer learning: CNN → foundation vision models, RNN → Transformers → LLMs.
- D: ✗ The lecture stresses convergence.

**Q35 → B, C, D**

The goal is to distill information by downsampling each channel. In AlexNet, 3×3 max pooling with stride 2 gives overlapping pooling.

- A: ✗ Pooling downsamples height and width. Channel count comes from the number of conv filters.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.

**Q36 → A**

Parameters per filter = k_h · k_w · C_in + 1 bias. Multiply by the number of filters. Height and width of the input do not matter.

- A: ✓ Correct. (3·3·64 + 1) · 128.
- B: ✗ This forgets the 128 biases.
- C: ✗ That would be a 1×1 convolution: (64 + 1) · 128.
- D: ✗ Each output channel has its own filter, spanning all 64 input channels.

**Q37 → C**

With stride 2 and padding='same', the output size is ceil(input/2), which is why the autoencoder encoder halves 32 → 16 → 8 → 4.

- A: ✗ That is padding='valid'.
- B: ✗ Unrelated to padding.
- C: ✓ Correct.
- D: ✗ Keras uses zero padding, not reflection.

**Q38 → B, C, D**

Benefits: rich visual knowledge, avoiding overfitting on small data, high performance from little data. Trade-off: limited domain specialization, which fine-tuning addresses. The COVID-19 chest X-ray paper is the real-world example given.

- A: ✗ Limited specialization to the target domain is listed as a trade-off.
- B: ✓ Correct, as it would overfit and be too costly.
- C: ✓ Correct.
- D: ✓ Correct.

**Q39 → A**

Steps: load model → remove head → add custom layers → freeze feature-extraction weights → train only the new layers.

- A: ✓ Correct.
- B: ✗ It has not been trained for the new task yet.
- C: ✗ That throws away the pretrained knowledge.
- D: ✗ The new head must stay trainable.

**Q40 → B**

A: input pixels → B: low-level edges → C: mid-level parts → D: high-level concepts. Features are learned from data, not hand-coded.

- A: ✗ That is unit B.
- B: ✓ Correct.
- C: ✗ That is unit D.
- D: ✗ That is unit A.

**Q41 → B**

DenseNet conv layers each produce 32 channels that are concatenated with earlier outputs, so channel count grows. Transition blocks compress it back.

- A: ✗ 1×1 convolutions do not change spatial size.
- B: ✓ Correct.
- C: ✗ DenseNet convolutions use batch normalization and ReLU.
- D: ✗ DenseNet connects by concatenation, not addition.


---

## SimCLR paper (Chen et al., 2020)

**Q42.** ☐ *Select all that apply.* Which are the four major components of the SimCLR framework? Select all that apply.

- ☐ **A.** A memory bank storing negative representations from previous batches so that many negatives are available
- ☐ **B.** A base encoder f(·), a ResNet, producing representation h
- ☐ **C.** A stochastic data augmentation module producing two correlated views (a positive pair)
- ☐ **D.** The NT-Xent contrastive loss
- ☐ **E.** A small MLP projection head g(·) mapping h to z, where the loss is applied

**Q43.** ○ *Single answer.* With a minibatch of N = 4096 images, how many negative examples does each positive pair have in SimCLR?

- ○ **A.** 8,192
- ○ **B.** 8,190, i.e., 2(N − 1)
- ○ **C.** None; negatives are sampled explicitly from a separate pool
- ○ **D.** 4,095

**Q44.** ○ *Single answer.* The NT-Xent loss for a positive pair (i, j) is ℓ_ij = −log [ exp(sim(z_i, z_j)/τ) / Σ_{k≠i} exp(sim(z_i, z_k)/τ) ]. What is sim(·,·), and what does the temperature τ do?

- ○ **A.** sim is the raw unnormalized dot product; τ is a margin that must be exceeded
- ○ **B.** sim is cosine similarity; τ scales the logits and sets how much hard negatives count
- ○ **C.** sim is the Euclidean distance; τ is the learning rate
- ○ **D.** sim is KL divergence between the two views’ projection-head outputs treated as probability distributions

**Q45.** ☐ *Select all that apply.* Which findings about data augmentation in SimCLR are correct? Select all that apply.

- ☐ **A.** Random cropping composed with color distortion stands out as the most effective pair
- ☐ **B.** AutoAugment, found via supervised search, clearly beat simple crop + strong color distortion for SimCLR
- ☐ **C.** No single transformation suffices to learn good representations
- ☐ **D.** Contrastive learning benefits from stronger color augmentation than supervised learning does
- ☐ **E.** Without color distortion, crops share color histograms, giving the network a shortcut

**Q46.** ○ *Single answer.* SimCLR compares three projection heads: identity, linear, and a nonlinear one-hidden-layer MLP. What did it find?

- ○ **A.** Linear and nonlinear heads perform identically, and z = g(h) is the better representation to keep for downstream tasks after pretraining
- ○ **B.** Nonlinear beats linear (~3%) and identity (>10%); h before the head beats z downstream
- ○ **C.** Performance depends strongly on the output dimension of z
- ○ **D.** No projection head is best, since any head discards information

**Q47.** ○ *Single answer.* Why does SimCLR use global batch normalization across devices during distributed training?

- ○ **A.** To reduce memory usage on each TPU core by storing the batch statistics only once, centrally
- ○ **B.** Because LARS cannot work with local batch statistics and diverges immediately at batch size 256 unless every device shares them
- ○ **C.** Positive pairs share a device, so per-device BN statistics leak a shortcut
- ○ **D.** To make the model invariant to color distortion

**Q48.** ☐ *Select all that apply.* Which statements about batch size, training length and optimization in SimCLR are correct? Select all that apply.

- ☐ **A.** Contrastive learning benefits less than supervised learning from longer training, so 100 epochs is close to optimal for it
- ☐ **B.** The LARS optimizer is used to stabilize large-batch training
- ☐ **C.** The default setup trains at batch size 256 for 1,000 epochs with plain SGD and no warmup
- ☐ **D.** Larger batches help most when training is short (e.g., 100 epochs); the gap shrinks with longer training
- ☐ **E.** Square-root learning-rate scaling can help, particularly for smaller batch sizes

**Q49.** ○ *Single answer.* Under the linear evaluation protocol on ImageNet, what did SimCLR with ResNet-50 (4×) achieve?

- ○ **A.** 76.5% top-1, matching a supervised ResNet-50
- ○ **B.** 85.8% top-1 with no labels at all
- ○ **C.** 69.3% top-1, which already matched a fully supervised ResNet-50 trained for 90 epochs
- ○ **D.** 92.6% top-1

**Q50.** ○ *Single answer.* What is the purpose of the linear evaluation protocol?

- ○ **A.** To fine-tune the entire network end-to-end with all labels
- ○ **B.** To compress the model into a linear network for deployment on mobile devices
- ○ **C.** To evaluate how many positive pairs the network correctly identifies among the 2N − 2 negatives in the contrastive task
- ○ **D.** To score representation quality with a linear classifier on the frozen encoder

**Q51.** ○ *Single answer.* Which statement about model size in SimCLR is correct?

- ○ **A.** Width helps but depth hurts contrastive learning, because deeper encoders tend to cause representation collapse
- ○ **B.** Both benefit, but the supervised–SimCLR gap shrinks as models grow
- ○ **C.** Model size has no measurable effect beyond ResNet-18
- ○ **D.** Bigger models help supervised learning but hurt contrastive learning

**Q52.** ○ *Single answer.* SimCLR is contrasted with generative approaches to representation learning. Which description fits SimCLR?

- ○ **A.** It requires image–text pairs, like CLIP
- ○ **B.** It generates or models pixels in input space, as autoencoders and GANs do
- ○ **C.** It relies on hand-designed pretext tasks such as rotation prediction or jigsaw puzzles
- ○ **D.** It is discriminative: it contrasts views of one image against other images

**Q53.** ○ *Single answer.* In SimCLR, how are two augmented views of the same image produced?

- ○ **A.** Two operators t and t′ are sampled independently from the augmentation family T
- ○ **B.** A GAN generates the second view
- ○ **C.** The same augmentation t is applied twice, giving identical views
- ○ **D.** One view is the original image and the other is augmented in the default training setup

**Q54.** ○ *Single answer.* With ℓ2 normalization removed from NT-Xent (raw dot products), what happened?

- ○ **A.** Training diverged immediately and no model could be trained at any temperature value
- ○ **B.** Contrastive accuracy and linear-evaluation accuracy both rose
- ○ **C.** Contrastive accuracy rose, but linear-evaluation accuracy got worse
- ○ **D.** Nothing changed

**Q55.** ☐ *Select all that apply.* Which loss functions did SimCLR compare against NT-Xent, and what was found? Select all that apply.

- ☐ **A.** Margin triplet loss
- ☐ **B.** NT-Xent required semi-hard negative mining to reach its best result, just as the other losses did
- ☐ **C.** Semi-hard negative mining helped the alternatives but still left them well below NT-Xent
- ☐ **D.** NT-Logistic loss

**Q56.** ○ *Single answer.* On transfer to other image classification datasets via fine-tuning, how did SimCLR compare with a strong supervised baseline?

- ○ **A.** It could not be fine-tuned
- ○ **B.** Better on all 12 datasets by more than ten points each, making supervised pretraining obsolete
- ○ **C.** It was worse on every dataset
- ○ **D.** On par or better on 10 of 12 datasets

**Q57.** ○ *Single answer.* Which encoder is used in the paper, and where is h taken from?

- ○ **A.** A ResNet; h is the output of the projection head’s final layer, the 128-d vector z
- ○ **B.** A ResNet; h is the output after the average-pooling layer
- ○ **C.** A ViT; h is the [class] token
- ○ **D.** An LSTM over image patches


### Answer key — SimCLR paper (Chen et al., 2020)

**Q42 → B, C, D, E**

SimCLR needs neither specialized architectures nor a memory bank. Two augmentations t, t′ ∼ T create x̃_i, x̃_j; f and g are trained to maximize agreement; after training g is discarded and h = f(x̃) is used downstream.

- A: ✗ SimCLR deliberately avoids memory banks and uses in-batch negatives with large batches.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✓ Correct.

**Q43 → B**

The paper’s example: batch size 8192 gives 16,382 negatives per positive pair. Large batches therefore supply many negatives, which is why SimCLR benefits from them.

- A: ✗ That is 2N, which incorrectly includes the anchor and its positive.
- B: ✓ Correct. There are 2N augmented views; excluding the anchor and its positive leaves 2N − 2.
- C: ✗ SimCLR does not sample negatives explicitly. The other in-batch views act as negatives.
- D: ✗ This counts only one view per image. Each image contributes two augmented views.

**Q44 → B**

NT-Xent stands for normalized temperature-scaled cross entropy. Looking at the gradients, ℓ2 normalization plus temperature weights negatives by their relative hardness, so it avoids the semi-hard negative mining that margin and logistic losses need. Linear evaluation: NT-Xent 63.9% versus at best 57.9% for the alternatives.

- A: ✗ Removing ℓ2 normalization raises contrastive accuracy but gives worse representations. A margin belongs to triplet losses.
- B: ✓ Correct. Table 5 shows τ ≈ 0.1 with ℓ2 normalization works best at batch 4096.
- C: ✗ sim is cosine similarity and τ is not a learning rate.
- D: ✗ No KL divergence is involved.

**Q45 → A, C, D, E**

Augmentations define the predictive task. Composing them makes the contrastive task harder but the representation better. Random crops subsume both global-to-local and adjacent-view prediction tasks.

- A: ✓ Correct.
- B: ✗ AutoAugment did not work better than crop + stronger color distortion.
- C: ✓ Correct. Composition is crucial.
- D: ✓ Correct. Table 1: SimCLR rises from 59.6 to 64.5 as strength increases, while supervised stays roughly flat.
- E: ✓ Correct. Figure 6 shows histograms alone can distinguish images.

**Q46 → B**

Hypothesis: the contrastive loss makes z invariant to augmentations, so g removes information (color, orientation) that may be useful downstream. Table 3 confirms h retains much more information about the applied transformation (e.g., rotation: 67.6% from h versus 25.6% from g(h)). Hence g is thrown away after pretraining.

- A: ✗ Nonlinear wins, and h beats z by more than 10%.
- B: ✓ Correct.
- C: ✗ With a head, results are similar regardless of the output dimension.
- D: ✗ No head was the worst, by more than 10%.

**Q47 → C**

Alternatives mentioned in the paper: shuffling examples across devices (MoCo) or replacing BN with layer norm (CPC v2).

- A: ✗ Global BN adds communication; it does not save memory.
- B: ✗ LARS addresses large-batch stability, not BN leakage.
- C: ✓ Correct. Aggregating BN mean and variance over all devices removes the shortcut.
- D: ✗ Unrelated to color invariance.

**Q48 → B, D, E**

Contrastive learning benefits more than its supervised counterpart from larger batches and longer training, which supply more negatives and more augmentation variety.

- A: ✗ It benefits more. Training up to 1,000 epochs keeps improving SimCLR, while supervised ResNets stop improving.
- B: ✓ Correct. Standard SGD/momentum with linear LR scaling can be unstable at large batch sizes.
- C: ✗ Default: batch 4096, 100 epochs, LARS with LR 4.8 = 0.3 × BatchSize/256, weight decay 10⁻⁶, 10-epoch warmup and cosine decay.
- D: ✓ Correct (Figure 9).
- E: ✓ Correct. Appendix B.1 covers square-root scaling.

**Q49 → A**

Linear evaluation trains a linear classifier on top of the frozen encoder and uses its test accuracy as a proxy for representation quality. ResNet-50 (1×) SimCLR: 69.3% top-1. ResNet-50 (4×): 76.5%. Semi-supervised with 1% labels: 75.5% top-5 (ResNet-50) and 85.8% (4×).

- A: ✓ Correct.
- B: ✗ 85.8% is top-5 accuracy when fine-tuning with 1% of labels.
- C: ✗ 69.3% is standard ResNet-50 SimCLR, and it does not match supervised.
- D: ✗ 92.6% is the top-5 accuracy with 10% labels for ResNet-50 (4×).

**Q50 → D**

Because the encoder is frozen and the classifier is linear, accuracy reflects how linearly separable, and therefore how useful, the learned features are.

- A: ✗ That is full fine-tuning, a separate experiment.
- B: ✗ Unrelated.
- C: ✗ Contrastive accuracy can be high while representations are poor (e.g., without ℓ2 normalization).
- D: ✓ Correct.

**Q51 → B**

The lecture: wider and deeper encoders improve representation quality, and contrastive learning benefits even more from them than supervised learning does.

- A: ✗ Depth also helps.
- B: ✓ Correct (Figure 7).
- C: ✗ Larger models give clear gains.
- D: ✗ Both benefit.

**Q52 → D**

The paper divides approaches into generative (pixel-level generation, which is expensive) and discriminative (pretext tasks or contrastive learning). Contrastive learning in the latent space achieved state-of-the-art results.

- A: ✗ SimCLR uses images only.
- B: ✗ Pixel-level generation is computationally expensive and not needed for representation learning.
- C: ✗ SimCLR avoids heuristic pretext tasks, which can limit generality.
- D: ✓ Correct.

**Q53 → A**

Default augmentations: random crop and resize (with flip), color distortion and Gaussian blur, applied sequentially.

- A: ✓ Correct.
- B: ✗ No generative model is involved.
- C: ✗ Identical views make the task trivial.
- D: ✗ That asymmetric setup was only used in the ablation, and it hurt performance.

**Q54 → C**

Table 5: with normalization and τ = 0.1, top-1 is 64.4%. Without normalization, contrastive accuracy is above 91% but top-1 is about 57%. Solving the pretext task better does not mean better features.

- A: ✗ Training ran, but the representations were worse.
- B: ✗ Only contrastive accuracy rose.
- C: ✓ Correct.
- D: ✗ Performance dropped significantly.

**Q55 → A, C, D**

The gradient analysis shows cross-entropy with ℓ2 normalization and temperature weights negatives by relative hardness; logistic and margin losses do not.

- A: ✓ Correct, one of the alternatives.
- B: ✗ NT-Xent weights negatives by hardness automatically and needs no mining.
- C: ✓ Correct. Their best was 57.9% versus 63.9%.
- D: ✓ Correct, one of the alternatives.

**Q56 → D**

The lecture: representations transfer strongly and match or exceed supervised pretraining on many datasets.

- A: ✗ Fine-tuning was evaluated.
- B: ✗ Too strong a claim.
- C: ✗ Not the result.
- D: ✓ Correct.

**Q57 → B**

The default projection head is a 2-layer MLP mapping the 2048-d h to a 128-d z. The framework places no constraints on the encoder architecture.

- A: ✗ That is z, which is not used downstream.
- B: ✓ Correct. For ResNet-50, h is 2048-dimensional.
- C: ✗ SimCLR uses ResNet.
- D: ✗ Not used.


---

## Class 3 · Autoencoders & VAEs

**Q58.** ○ *Single answer.* A latent variable model describes Pr(x) indirectly. Which expression is the marginalization used for a continuous latent z?

- ○ **A.** Pr(x) = ∫ Pr(x | z) Pr(z) dz
- ○ **B.** Pr(x) = max_z Pr(x, z), taking only the single most likely latent configuration for each observed data point
- ○ **C.** Pr(x) = Pr(x | z) for z = 0
- ○ **D.** Pr(x) = Pr(z | x) Pr(x) / Pr(z)

**Q59.** ☐ *Select all that apply.* Consider the 1-D mixture of Gaussians viewed as a latent variable model. Which statements are correct? Select all that apply.

- ☐ **A.** The mixing weights λ_n may be negative as long as they sum to one
- ☐ **B.** Pr(x | z = n) is normal with mean μ_n and variance σ_n²
- ☐ **C.** Pr(x) is obtained by summing the weighted components: Σ_n λ_n · Norm(x; μ_n, σ_n²)
- ☐ **D.** Pr(x) must be unimodal, since each individual component is a single Gaussian with only one peak
- ☐ **E.** z is discrete, and the prior Pr(z) is categorical with probabilities λ_n

**Q60.** ○ *Single answer.* Why is training the nonlinear latent variable model by direct maximum likelihood intractable?

- ○ **A.** The decoder f[z, φ] is not differentiable with respect to its parameters, so gradients cannot be computed
- ○ **B.** The likelihood Pr(x|z) is not Gaussian, so no parametric form exists for evaluating it at all
- ○ **C.** The prior Pr(z) is unknown and must be learned jointly with φ, which makes the objective ill-posed in high dimensions
- ○ **D.** The integral ∫ Pr(x|z, φ) Pr(z) dz has no closed form and is hard to evaluate for a given x

**Q61.** ☐ *Select all that apply.* Which statements about the Evidence Lower Bound (ELBO) are correct? Select all that apply.

- ☐ **A.** Maximizing it with respect to θ can decrease the true log-likelihood while increasing the bound itself
- ☐ **B.** It depends on decoder parameters φ and variational parameters θ
- ☐ **C.** It lies everywhere below the log-likelihood log Pr(x|φ)
- ☐ **D.** It is tight when q(z|x, θ) equals the true posterior Pr(z|x, φ)
- ☐ **E.** It can be written as reconstruction term − KL(q(z|x,θ) ‖ Pr(z))

**Q62.** ☐ *Select all that apply.* Which statements about KL divergence, as presented in the lecture, are correct? Select all that apply.

- ☐ **A.** It is symmetric, KL(p ‖ q) = KL(q ‖ p), so it is a true distance metric satisfying the triangle inequality
- ☐ **B.** KL(p ‖ q) explodes to infinity if p assigns positive probability where q assigns zero
- ☐ **C.** It measures the information lost when q is used to approximate p
- ☐ **D.** It is always ≥ 0, and equals 0 only when the two distributions are identical

**Q63.** ○ *Single answer.* The VAE encoder outputs z_mean and z_log_var. What is the closed-form KL term to N(0, I) used in the implementation?

- ○ **A.** 0.5 · Σ (z_mean² + z_log_var²), the squared distance of the encoder outputs from the origin
- ○ **B.** −0.5 · Σ (1 + z_log_var − z_mean² − exp(z_log_var))
- ○ **C.** Σ (z_mean − z_log_var)²
- ○ **D.** −Σ log(z_mean)

**Q64.** ○ *Single answer.* Why does the VAE encoder output the log of the variance rather than the variance itself?

- ○ **A.** Log variance makes the KL term vanish, which leaves only the reconstruction loss to optimize
- ○ **B.** To make the latent dimensions correlated with one another, giving a full covariance matrix
- ○ **C.** Network outputs are unbounded but variance must be positive; exp(log_var) is always > 0
- ○ **D.** The log variance is required by the reparameterization trick, which only accepts values in (0, 1)

**Q65.** ○ *Single answer.* What does the reparameterization trick z = μ + σ ⊙ ε, with ε ~ N(0, I), accomplish?

- ○ **A.** It removes all randomness from the VAE, making it deterministic
- ○ **B.** It isolates randomness in ε so z is differentiable in μ and σ
- ○ **C.** It forces the encoder to output a full covariance matrix, capturing correlations between latent dimensions
- ○ **D.** It replaces the KL term in the loss

**Q66.** ☐ *Select all that apply.* The plain autoencoder trained on Fashion-MNIST with a 2-D latent space produced a problematic embedding. Which observations did the lecture list? Select all that apply.

- ☐ **A.** There are large gaps between clusters containing few points
- ☐ **B.** The distribution is not symmetric about (0, 0); many points have large positive y-values
- ☐ **C.** Points decoded from anywhere in the bounding box are guaranteed to look like realistic, well-formed clothing items
- ☐ **D.** Some clothing items occupy a very small area and others a much larger one

**Q67.** ○ *Single answer.* How does the VAE’s encoder differ from a plain autoencoder’s encoder?

- ○ **A.** The VAE encoder outputs class labels that the decoder then uses to choose which clothing type to draw
- ○ **B.** The VAE has no encoder; it samples latent vectors from the prior and then optimizes them directly with gradient descent
- ○ **C.** The AE maps each image to one point; the VAE maps it to a normal distribution around a point
- ○ **D.** The VAE encoder uses transposed convolutions

**Q68.** ☐ *Select all that apply.* Which effects of the KL loss term on the latent space are described in the lecture? Select all that apply.

- ☐ **A.** It reduces the chance of large gaps forming between point clusters
- ☐ **B.** It provides a well-defined distribution, N(0, I), from which to choose latent points for generation
- ☐ **C.** It forces each clothing class into its own separate region, since the KL term acts as a supervised class-separation loss
- ☐ **D.** It guarantees perfect pixel-level reconstructions
- ☐ **E.** It encourages the encoder to use the space around the origin symmetrically and efficiently

**Q69.** ○ *Single answer.* For the CelebA VAE, what changes were made compared to the Fashion-MNIST model?

- ○ **A.** Latent dimension 2, β = 0.001, and the decoder replaced by a GAN generator trained adversarially on the celebrity images
- ○ **B.** 3 input channels, latent dimension increased from 2 to 200, KL β factor of 2,000, batch norm after each conv
- ○ **C.** Latent dimension reduced to 1, grayscale input, β removed
- ○ **D.** Removal of the encoder

**Q70.** ○ *Single answer.* How is a “smile vector” built and used in VAE latent-space arithmetic?

- ○ **A.** Train a separate classifier for smiling and use its weights as the vector
- ○ **B.** Subtract the average non-smiling embedding from the average smiling one; add α times it to any z
- ○ **C.** Multiply the latent vector element-wise by a mask that zeros out every dimension except the one known to encode smiling
- ○ **D.** Randomly sample until a smiling face appears

**Q71.** ○ *Single answer.* Morphing between faces A and B uses z_new = z_A(1 − α) + z_B α. What happens as α goes from 0 to 1?

- ○ **A.** The model is retrained on every interpolated point to make sure each intermediate face decodes realistically
- ○ **B.** Decoded images transition gradually from face A to face B
- ○ **C.** The output jumps abruptly from A to B at α = 0.5
- ○ **D.** The image becomes pure noise at α = 0.5, since the midpoint lies outside the learned latent distribution

**Q72.** ○ *Single answer.* Ancestral sampling for Pr(x, y, z) = Pr(x) Pr(y|x) Pr(z|y) proceeds by

- ○ **A.** drawing x* ~ Pr(x), then y* ~ Pr(y|x*), then z* ~ Pr(z|y*)
- ○ **B.** sampling z first, then y, then x
- ○ **C.** Gibbs sampling all three variables jointly, cycling through each conditional until the chain converges to the joint
- ○ **D.** computing the marginal of each variable separately

**Q73.** ○ *Single answer.* A Conv2DTranspose layer with stride 2 is used in the decoder. What does it do?

- ○ **A.** Performs max pooling followed by a learned 1×1 convolution, keeping the spatial size unchanged
- ○ **B.** Upsamples: it produces a larger spatial output, typically with fewer channels
- ○ **C.** Halves the spatial size and doubles channels
- ○ **D.** Computes attention between feature-map positions so that every spatial location can aggregate information from every other

**Q74.** ○ *Single answer.* The Fashion-MNIST encoder takes a 32×32×1 input through three Conv2D layers (32, 64, 128 filters, 3×3, stride 2, padding same), then Flatten, then Dense(2). What is the shape before Flatten, and how many parameters does Dense(2) have?

- ○ **A.** 2×2×128 → 512 features; Dense(2) has 1,026 parameters, since each stride-2 layer halves the spatial size twice
- ○ **B.** 4×4×128 → 2,048 features; Dense(2) has 4,096 parameters
- ○ **C.** 4×4×128 → 2,048 features; Dense(2) has 2,048·2 + 2 = 4,098 parameters
- ○ **D.** 8×8×128 → 8,192 features; Dense(2) has 16,386 parameters

**Q75.** ○ *Single answer.* Which loss did the lecture’s Keras autoencoder use, and why?

- ○ **A.** Binary cross-entropy, appropriate for pixel values scaled to [0, 1] with a sigmoid output
- ○ **B.** Categorical cross-entropy over the 10 clothing classes
- ○ **C.** Mean absolute error between the 2-D latent vectors of each image and its augmented copy, as in contrastive learning
- ○ **D.** Hinge loss, because the decoder outputs signed margins rather than pixel intensities

**Q76.** ☐ *Select all that apply.* ECMVAE (Explicit Conditional Multimodal VAE) for audio-visual segmentation. Which statements are correct? Select all that apply.

- ☐ **A.** It factorizes each modality’s latent into a shared code c and specific codes s_a, s_v
- ☐ **B.** It relies on implicit feature fusion so that the individual contribution of each modality stays hidden from the model
- ☐ **C.** It uses Jensen–Shannon divergence to balance sampling efficiency and generation quality
- ☐ **D.** A mutual-information maximization regularizer encourages maximally informative representations
- ☐ **E.** An orthogonality constraint keeps shared and specific codes exclusive and prevents information leakage

**Q77.** ○ *Single answer.* In ECMVAE’s view of multimodal information for audio-visual segmentation, what does the audio modality mainly contribute?

- ○ **A.** Scene context, in which the candidate sound producers usually occupy only a small portion of the frame
- ○ **B.** Category information about what kind of sound, and so what kind of source, is present
- ○ **C.** Nothing; the audio is used only as a regularizer
- ○ **D.** Precise pixel locations of sound producers

**Q78.** ○ *Single answer.* AVSBench evaluation settings S4 and MS3 refer to

- ○ **A.** Four-second and three-second clip lengths used for the single-frame and the multi-frame subsets
- ○ **B.** Spatial and Spectral metrics, measuring mask overlap and audio-frequency alignment respectively
- ○ **C.** Supervised and Multi-Shot training settings in which the number of labeled frames per video is varied
- ○ **D.** Single-Sound-Source segmentation and Multiple-Sound-Source segmentation

**Q79.** ○ *Single answer.* In the nonlinear latent variable model, which parts of the data are explained by f[z, φ] and which by σ²I?

- ○ **A.** f explains the noise, and σ²I explains the structure
- ○ **B.** f models the important structure; leftover detail is treated as spherical noise σ²I
- ○ **C.** σ²I is learned per pixel
- ○ **D.** Both model noise, because the latent z is pure noise and carries no information about the data

**Q80.** ○ *Single answer.* Bayes’ rule gives the posterior Pr(z | x, φ) = Pr(x|z, φ) Pr(z) / Pr(x|φ). Why is it not used directly in the VAE?

- ○ **A.** The posterior is always Gaussian, so it is unnecessary
- ○ **B.** The prior Pr(z) is unknown
- ○ **C.** The evidence Pr(x|φ) in the denominator is intractable
- ○ **D.** The likelihood is not differentiable with respect to z, which blocks every gradient-based method

**Q81.** ☐ *Select all that apply.* Which statements about the multivariate standard normal N(0, I) are correct? Select all that apply.

- ☐ **A.** The mean vector is all zeros
- ☐ **B.** The covariance matrix may be asymmetric, with cov(X, Y) ≠ cov(Y, X) when the variables are dependent
- ☐ **C.** Off-diagonal covariances are zero, so for a Gaussian the variables are independent
- ☐ **D.** The covariance is the identity matrix, so each variable has unit variance

**Q82.** ○ *Single answer.* Why does the plain autoencoder struggle to generate new images by sampling random latent points?

- ○ **A.** It has no decoder, so there is no network that maps a latent point back into the image space
- ○ **B.** Its encoder is stochastic
- ○ **C.** Its latent space is not forced to be continuous, so random points often decode poorly
- ○ **D.** Its decoder cannot accept inputs outside the training set

**Q83.** ○ *Single answer.* In the “infinite wardrobe” analogy, what does the VAE change compared with the plain autoencoder?

- ○ **A.** Items are sorted alphabetically
- ○ **B.** Each item gets a general area, kept near the center and limited in size
- ○ **C.** Each item is placed at one exact location, as before
- ○ **D.** The stylist is replaced by a second wardrobe so that every outfit is stored twice on opposite sides


### Answer key — Class 3 · Autoencoders & VAEs

**Q58 → A**

Latent variable models define a joint Pr(x, z) = Pr(x|z)Pr(z): a likelihood times a prior. For a discrete z (mixture of Gaussians) the integral becomes a sum Σ_n λ_n Norm(x; μ_n, σ_n²). For the nonlinear LVM, Pr(x|φ) = ∫ Norm(x; f[z, φ], σ²I) Norm(z; 0, I) dz, an infinite mixture of spherical Gaussians.

- A: ✓ Correct. Integrate the joint Pr(x, z) = Pr(x|z)Pr(z) over z.
- B: ✗ Taking a max gives a MAP-style approximation, not the marginal likelihood.
- C: ✗ Evaluating at one latent point ignores the prior and all other latents.
- D: ✗ This is a garbled Bayes’ rule. It contains Pr(x) on both sides and does not marginalize anything.

**Q59 → B, C, E**

The slides’ example: “Gaussian 1 gets 70% weight, Gaussian 2 gets 20%, Gaussian 3 gets 10%.” Complexity grows with more components. The nonlinear latent variable model generalizes this to a continuous z and an infinite mixture.

- A: ✗ λ_n are probabilities: non-negative and summing to 1.
- B: ✓ Correct.
- C: ✓ Correct. This is marginalization over the discrete z.
- D: ✗ Mixing several Gaussians with different means produces multiple peaks. That is the whole point of a mixture.
- E: ✓ Correct.

**Q60 → D**

Because the marginal likelihood is an integral over a nonlinear network’s outputs, there is no closed-form expression and no easy way to evaluate it. The fix is a lower bound (the ELBO) that can be maximized with respect to both φ (decoder) and θ (variational/encoder parameters).

- A: ✗ Neural networks are differentiable. That is not the obstacle.
- B: ✗ In this model Pr(x|z) is Gaussian by construction.
- C: ✗ The prior is fixed to a standard normal Norm(0, I).
- D: ✓ Correct. This is why we introduce the ELBO.

**Q61 → B, C, D, E**

Optimization moves both between colored curves (improving θ tightens the bound) and along them (improving φ raises the likelihood). The VAE loss is the negative ELBO, minimized with SGD or Adam using automatic differentiation.

- A: ✗ Changing θ only changes the bound (moves between curves). The log-likelihood depends on φ alone.
- B: ✓ Correct. For fixed θ it is a function of φ alone (the colored curves).
- C: ✓ Correct, which is why it is called a lower bound.
- D: ✓ Correct. The gap is KL(q ‖ posterior).
- E: ✓ Correct. This is the reconstruction-minus-distance-to-prior view.

**Q62 → B, C, D**

KL(p ‖ q) = Σ p(x) log[p(x)/q(x)]. The zero-probability issue causes undefined or extreme gradients and can push q toward degenerate predictions. In the VAE, KL(q(z|x) ‖ N(0, I)) regularizes the latent space.

- A: ✗ KL is asymmetric and violates the triangle inequality, so it is a divergence, not a metric.
- B: ✓ Correct. This is the “infinity trap” on the slide.
- C: ✓ Correct.
- D: ✓ Correct.

**Q63 → B**

Per dimension, KL(N(μ, σ²) ‖ N(0, 1)) = ½(μ² + σ² − log σ² − 1). With log σ² = z_log_var this becomes −½(1 + z_log_var − μ² − e^{z_log_var}). It is zero when μ = 0 and σ = 1, which pulls encoded distributions toward the origin.

- A: ✗ This is not the Gaussian KL and ignores the variance term entirely.
- B: ✓ Correct. This is the analytic KL between a diagonal Gaussian and the standard normal.
- C: ✗ Not a KL divergence.
- D: ✗ Undefined for negative means and not a KL divergence.

**Q64 → C**

z_sigma = exp(z_log_var · 0.5). The encoder ignores covariance between latent dimensions, so it outputs only mean and log-variance vectors that define a diagonal multivariate normal.

- A: ✗ It does not. The KL term still depends on the variance.
- B: ✗ The encoder assumes zero correlation (diagonal covariance).
- C: ✓ Correct.
- D: ✗ The reparameterization trick needs σ, which is computed as exp(0.5 · log_var). There is no (0, 1) restriction.

**Q65 → B**

Sampling z ~ q(z|x) directly is non-differentiable with respect to the encoder parameters. Writing z = g(ε, x) with fixed-distribution noise turns it into a deterministic, differentiable transform, which makes backpropagation possible (Kingma & Welling, 2013).

- A: ✗ Randomness remains, but it is isolated in ε.
- B: ✓ Correct.
- C: ✗ The VAE encoder uses a diagonal covariance.
- D: ✗ Both the reconstruction and KL terms remain.

**Q66 → A, B, D**

Because nothing forces the latent space to be continuous, nearby points (e.g., (−2, 2) and (−2.1, 2.1)) need not decode to similar images, and sampling uniformly between min and max embeddings gives poor results. The VAE fixes this with neighborhood sampling plus the KL term.

- A: ✓ Correct (sparse gaps).
- B: ✓ Correct (asymmetry).
- C: ✗ The opposite: gaps mean random samples often decode to poorly formed images.
- D: ✓ Correct (variable density).

**Q67 → C**

Sampling around z_mean forces the decoder to produce similar images for nearby latent points, which gives continuity. The KL loss keeps those regions near the origin and limits their size, so there are fewer gaps. The decoder itself is identical to a plain autoencoder’s.

- A: ✗ VAEs are trained without labels.
- B: ✗ That is closer to GLO-style latent optimization.
- C: ✓ Correct.
- D: ✗ Transposed convolutions are in the decoder of both models.

**Q68 → A, B, E**

Loss = reconstruction loss + β · KL. The reconstruction term rewards fidelity, while the KL term regularizes toward the standard normal, giving a continuous, centered, gap-free latent space.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✗ Labels are never used. The VAE latent visualization shows each category roughly equally represented, with no preferential treatment.
- D: ✗ The KL term trades off against reconstruction and generally makes reconstructions blurrier.
- E: ✓ Correct.

**Q69 → B**

Faces are more complex than clothing, so they need more latent capacity (200 dimensions) and a stronger β to balance reconstruction against regularization. Batch normalization increases per-batch time but reduces the number of batches needed to converge.

- A: ✗ No GAN is involved, and the latent dimension was increased.
- B: ✓ Correct.
- C: ✗ All three are opposite to what was done.
- D: ✗ The encoder is still required.

**Q70 → B**

Labeled attributes (CelebA has 40) are used only after training to locate concept directions. The scalar α controls the strength of the change. Subtracting the vector removes the feature.

- A: ✗ No classifier weights are used.
- B: ✓ Correct. z_new = z + α · feature_vector.
- C: ✗ Features are not axis-aligned to a single known dimension.
- D: ✗ That is not arithmetic.

**Q71 → B**

Linear interpolation is meaningful only because the VAE latent space is continuous. In a plain AE, the straight line might cross empty gaps and decode to artifacts.

- A: ✗ No retraining is needed. Interpolation happens at inference time.
- B: ✓ Correct. Each intermediate point decodes to a new face.
- C: ✗ A continuous latent space yields gradual transitions.
- D: ✗ In a well-regularized VAE, interior points decode to plausible faces.

**Q72 → A**

For the nonlinear LVM, draw z* from the prior N(0, I), pass it through f[z*, φ] to get the mean of Pr(x|z*), then draw x*. Both distributions are normal, so this is straightforward. Diffusion models also generate this way, walking z_T → z_{T−1} → … → x.

- A: ✓ Correct.
- B: ✗ This goes against the factorization order.
- C: ✗ Gibbs sampling is a different (MCMC) method.
- D: ✗ That ignores the dependencies between variables.

**Q73 → B**

Transposed (fractionally strided) convolutions take a smaller spatial input with more channels and produce a larger output with fewer channels. The filter count sets the output channels. The decoder mirrors the encoder: Dense → Reshape → Conv2DTranspose stack → final Conv2D with sigmoid.

- A: ✗ Pooling downsamples and has no learnable kernel.
- B: ✓ Correct.
- C: ✗ That is what a stride-2 convolution does in the encoder.
- D: ✗ Attention is a different operation.

**Q74 → C**

With padding 'same' and stride 2, each conv halves height and width. Flatten has no parameters. Dense parameters = inputs × outputs + outputs (biases). The resulting 2-D latent space is what gets visualized.

- A: ✗ Each stride-2 layer halves the size once.
- B: ✗ This forgets the 2 bias terms.
- C: ✓ Correct. 32 → 16 → 8 → 4 spatially, with 128 channels.
- D: ✗ There are three stride-2 halvings: 32 → 16 → 8 → 4, not 8.

**Q75 → A**

autoencoder.compile(optimizer='adam', loss='binary_crossentropy'); fit(x_train, x_train, epochs=5, batch_size=100). The target equals the input because the network learns to reconstruct.

- A: ✓ Correct.
- B: ✗ The autoencoder reconstructs pixels and never uses the class labels.
- C: ✗ There is no augmentation or latent comparison. The model is trained with x_train as both input and target.
- D: ✗ Hinge loss is for margin classifiers.

**Q76 → A, C, D, E**

Components: a visual backbone (ImageNet-pretrained plus a conv neck); a frozen VGGish audio encoder (AudioSet); three latent encoders φ_sv, φ_sa, φ_c; and a decoder with TPAVI cross-modal attention producing pixel-wise masks. The objective is the ELBO (reconstruction plus KL) with the extra constraints. On AVSBench it gains +3.00 and +3.84 mIoU on the S4 and MS3 settings (PVTv2 backbone).

- A: ✓ Correct.
- B: ✗ This is the limitation ECMVAE fixes. It explicitly models each modality’s contribution.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✓ Correct.

**Q77 → B**

Audio provides category information. Visual identifies candidate sound producers in the scene. The shared code corresponds to the actual target sound producers. Cross-modal learning is what makes AVS possible.

- A: ✗ That describes the visual modality.
- B: ✓ Correct.
- C: ✗ Audio carries critical category information.
- D: ✗ Localization comes mainly from the visual modality, combined with shared information.

**Q78 → D**

AVSBench has 5,356 video sequences with audio and binary per-pixel annotations. mIoU measures mask overlap; F-score combines precision and recall.

- A: ✗ Not clip lengths.
- B: ✗ The metrics are mIoU and F-score.
- C: ✗ Not training-regime labels.
- D: ✓ Correct.

**Q79 → B**

z is lower-dimensional than x, so f captures the important factors. Pr(x|φ) is an infinite mixture of spherical Gaussians weighted by Pr(z).

- A: ✗ This is reversed.
- B: ✓ Correct.
- C: ✗ In this model it is a spherical (shared) variance, assumed known.
- D: ✗ z carries the structure through f.

**Q80 → C**

Hence the variational approximation q(z|x, θ) = N(g_μ[x, θ], g_Σ[x, θ]) with a diagonal covariance, found by minimizing KL to the true posterior. That is equivalent to maximizing the ELBO.

- A: ✗ The true posterior is generally complex and non-Gaussian.
- B: ✗ The prior is the fixed standard normal.
- C: ✓ Correct.
- D: ✗ The likelihood is differentiable.

**Q81 → A, C, D**

A general multivariate normal N(μ, Σ) has a mean vector and a symmetric covariance matrix. The VAE prior is N(0, I) and the encoder outputs a diagonal Σ.

- A: ✓ Correct.
- B: ✗ Covariance matrices are always symmetric.
- C: ✓ Correct.
- D: ✓ Correct.

**Q82 → C**

There is no requirement for the latent space to be continuous, and it is uneven and asymmetric. VAEs add sampling around each mean and a KL penalty, which turns the autoencoder into a strong generative model.

- A: ✗ An autoencoder has a decoder.
- B: ✗ A plain AE encoder is deterministic.
- C: ✓ Correct.
- D: ✗ The decoder accepts any vector.

**Q83 → B**

Encoding to areas gives more diversity and avoids discontinuities. The constraints are the KL term: center the areas, limit their size, and penalize deviation.

- A: ✗ Not part of the analogy.
- B: ✓ Correct.
- C: ✗ That is the plain autoencoder.
- D: ✗ Not part of the analogy.


---

## Class 4 · Transformers

**Q84.** ○ *Single answer.* In scaled dot-product attention, Attention(Q, K, V) = softmax(QKᵀ / √d_k) V. Why divide by √d_k?

- ○ **A.** To reduce the number of parameters in W_Q and W_K
- ○ **B.** To make the attention weights sum to 1 across each row before the values are aggregated
- ○ **C.** Because additive attention requires it to remain numerically equivalent to multiplicative attention for any key dimension
- ○ **D.** Large d_k makes dot products large, pushing softmax into regions with tiny gradients; scaling counteracts this

**Q85.** ☐ *Select all that apply.* Which statements about queries, keys and values are correct? Select all that apply.

- ☐ **A.** Attention is a soft lookup: queries match all keys with weights in [0, 1]
- ☐ **B.** V holds per-position weights, and K holds the content that is ultimately summed into the output vector for each token
- ☐ **C.** Q, K and V are computed as XW_Q, XW_K and XW_V, where the W matrices are the learnable parameters
- ☐ **D.** Each query attends only to the single key with the highest score, and the other values are discarded
- ☐ **E.** The attention weight matrix softmax(QKᵀ/√d_k) has shape (n, n) for a sequence of length n

**Q86.** ○ *Single answer.* Why do Transformers need positional encodings?

- ○ **A.** To prevent the decoder from attending to future tokens
- ○ **B.** To reduce the memory cost of attention from quadratic to linear in sequence length
- ○ **C.** Self-attention has no recurrence or convolution, so it is permutation-invariant and order must be injected
- ○ **D.** Because word embeddings are too small to hold semantic content, so extra dimensions with position data are needed

**Q87.** ☐ *Select all that apply.* Which statements about multi-head attention are correct? Select all that apply.

- ☐ **A.** Different heads can track different relations, e.g., long-distance dependencies or anaphora
- ☐ **B.** Head outputs are concatenated and projected by a final matrix W_O
- ☐ **C.** All heads share one set of projection weights, so multiple heads only average out the noise in the attention scores
- ☐ **D.** Each head has its own W_Q, W_K, W_V, so heads can learn distinct attention patterns

**Q88.** ○ *Single answer.* What does the causal (look-ahead) mask do in decoder self-attention?

- ○ **A.** It masks out padding tokens only, leaving all real tokens visible in both directions so that the context is bidirectional
- ○ **B.** It sets scores for future positions to −∞ before softmax, so each token sees only earlier ones
- ○ **C.** It hides the encoder output from the decoder so that the model cannot copy the source sentence
- ○ **D.** It randomly drops 15% of tokens, as in BERT pretraining

**Q89.** ○ *Single answer.* In encoder–decoder cross-attention, where do Q, K and V come from?

- ○ **A.** Q from the previous decoder layer; K and V from the encoder output
- ○ **B.** Q, K and V all come from the encoder output, which is computed once and reused at each step
- ○ **C.** Q, K and V all come from the decoder’s own previous layer, as in self-attention
- ○ **D.** Q from the encoder output; K and V from the decoder layer below, so the encoder decides which decoded tokens matter

**Q90.** ☐ *Select all that apply.* Match Transformer families to their descriptions. Which pairings are correct? Select all that apply.

- ☐ **A.** Encoder-only models use causal masking and are therefore the natural first choice for open-ended, token-by-token text generation
- ☐ **B.** Encoder–decoder (T5, BART): maps one text sequence to another, e.g., translation and summarization
- ☐ **C.** Encoder-only (BERT, RoBERTa): bidirectional context; suited to classification and NER
- ☐ **D.** Decoder-only (GPT): left context only; generates by next-token prediction

**Q91.** ☐ *Select all that apply.* Which statements about BERT pretraining are correct? Select all that apply.

- ☐ **A.** MLM predicts masked tokens’ original ids using left and right context
- ☐ **B.** The input embedding is the sum of token, segment and position embeddings
- ☐ **C.** Pretraining data is BooksCorpus (800M words) plus English Wikipedia (2,500M words)
- ☐ **D.** In NSP, B is the true next sentence 50% of the time and random otherwise
- ☐ **E.** BERT-Large has 12 layers, hidden size 768 and 12 heads, for a total of roughly 110 million parameters

**Q92.** ○ *Single answer.* Which statement best describes T5 (Text-to-Text Transfer Transformer)?

- ○ **A.** An encoder-only model that outputs class probabilities
- ○ **B.** Every task is cast as text in, text out, with one encoder–decoder model
- ○ **C.** A vision–language model that converts images to captions by treating pixels as text tokens
- ○ **D.** A decoder-only model trained exclusively on code, which is later prompted with natural-language instructions

**Q93.** ☐ *Select all that apply.* Layer normalization in the Transformer. Which statements are correct? Select all that apply.

- ☐ **A.** For an input of shape [N, C, H, W], it computes statistics over [C, H, W] for each sample
- ☐ **B.** It normalizes each sample’s activations to zero mean and unit variance, independently per training case
- ☐ **C.** It computes the mean and variance across the batch dimension, so its behavior changes with batch size, like batch norm
- ☐ **D.** After normalization it applies learnable scale γ and shift β

**Q94.** ○ *Single answer.* According to Geva et al. (2020), what are Transformer feed-forward layers?

- ○ **A.** Redundant layers that can be removed without changing predictions, since attention alone determines the next token
- ○ **B.** Gating mechanisms equivalent to LSTM forget gates
- ○ **C.** Purely positional encoders that recompute each token’s position after every attention block
- ○ **D.** Key–value memories: keys detect input patterns, and values induce distributions over the output vocabulary

**Q95.** ☐ *Select all that apply.* Causal mediation analysis applied to neural networks. Which statements are correct? Select all that apply.

- ☐ **A.** Mediators are internal states such as neurons, layers or attention heads
- ☐ **B.** The independent variable is typically the model input and the dependent variable the model output
- ☐ **C.** The indirect effect is the part of the total effect that passes through the mediator
- ☐ **D.** The direct effect is measured by changing the mediator while holding the model input completely fixed

**Q96.** ☐ *Select all that apply.* MEMIT (Mass-Editing Memory in a Transformer). Which statements are correct? Select all that apply.

- ☐ **A.** Its goals include effectiveness, generalization to paraphrases, specificity and fluency
- ☐ **B.** It uses causal analysis to locate critical MLP layers on the factual-recall path and edits them
- ☐ **C.** It updates knowledge by retraining the whole model from scratch on a corrected corpus that contains the new facts
- ☐ **D.** It was validated on GPT-J and GPT-NeoX
- ☐ **E.** It inserts thousands of factual memories directly into the model weights in a batch

**Q97.** ○ *Single answer.* T-DMCA (Liu et al., 2018) modifies decoder self-attention for long sequences. What do its two components do?

- ○ **A.** Local attention removes the softmax, and memory-compressed attention removes positional encodings
- ○ **B.** Local attention uses blocks; memory-compressed attention shrinks K and V by strided conv
- ○ **C.** It replaces attention with an LSTM
- ○ **D.** Both components compress the queries, while keys and values stay at full length so no information is lost

**Q98.** ○ *Single answer.* Why does attention help with long-range dependencies compared to an RNN?

- ○ **A.** Any two positions connect directly, so gradients need not cross many time steps
- ○ **B.** It stores the entire past in a single fixed-size hidden vector, just as an RNN does but at a higher dimension
- ○ **C.** It removes the need for any training data
- ○ **D.** It uses fewer floating-point operations for every sequence length

**Q99.** ○ *Single answer.* He et al. (2016) describe a degradation problem in deep plain networks. What is it?

- ○ **A.** Images degrade after many convolutions because each filter blurs the signal a little more
- ○ **B.** Test error increases because of overfitting
- ○ **C.** Weights decay toward zero because of L2 regularization, which shrinks the effective capacity of every additional layer
- ○ **D.** Training error increases with depth even though a deeper network has more capacity

**Q100.** ○ *Single answer.* Additive attention and dot-product attention compared. Which statement matches Vaswani et al.?

- ○ **A.** Additive attention has no learnable parameters, which is why it is faster to train
- ○ **B.** Additive attention is much faster in practice
- ○ **C.** Dot-product attention always outperforms additive attention, with or without scaling, for every d_k
- ○ **D.** Similar complexity, but dot-product is faster and more memory-efficient

**Q101.** ○ *Single answer.* In GPT (Radford et al., 2018), how is the pretrained model adapted to downstream tasks?

- ○ **A.** By freezing all weights and using k-nearest neighbors on embeddings
- ○ **B.** By replacing the decoder with a BERT-style bidirectional encoder before fine-tuning on the labeled task data
- ○ **C.** By training a new model from scratch for each task
- ○ **D.** Supervised fine-tuning with task-specific input transformations and a new output layer

**Q102.** ○ *Single answer.* Pretraining a language model before fine-tuning adds an inductive bias. What does that mean here?

- ○ **A.** The model is biased toward the majority class
- ○ **B.** Language knowledge is preloaded, so it generalizes better with little task data
- ○ **C.** The model’s weights are randomly initialized for each task
- ○ **D.** The architecture is constrained to use convolutions, so that it is biased toward local patterns in text

**Q103.** ○ *Single answer.* For BERT-Base (H = 768, A = 12), what is the dimension of each attention head?

- ○ **A.** 64
- ○ **B.** 1,024
- ○ **C.** 768
- ○ **D.** 12, because each head works with one dimension per layer, and BERT-Base has twelve layers

**Q104.** ○ *Single answer.* For a sequence of n tokens, how do the memory and compute of the self-attention score matrix scale?

- ○ **A.** O(n²)
- ○ **B.** O(1)
- ○ **C.** O(n)
- ○ **D.** O(log n), because softmax normalizes each row and so only a few entries ever need to be stored

**Q105.** ☐ *Select all that apply.* Which statements about the sinusoidal positional encoding are correct? Select all that apply.

- ☐ **A.** The encoding is learned by backpropagation together with the token embeddings during pretraining
- ☐ **B.** PE_{pos+k} is a linear function of PE_pos for any fixed offset k
- ☐ **C.** The wavelengths form a geometric progression from 2π to 10000·2π
- ☐ **D.** Each dimension corresponds to a sinusoid of a different frequency

**Q106.** ○ *Single answer.* In causal mediation analysis, how is the direct effect estimated?

- ○ **A.** Vary the input while holding the mediator fixed
- ○ **B.** Remove the output layer
- ○ **C.** Clamp the input and change only the mediator, measuring how far the output moves
- ○ **D.** Vary the input and let all mediators change freely

**Q107.** ☐ *Select all that apply.* Which factual-recall mechanism did MEMIT’s causal analysis find? Select all that apply.

- ☐ **A.** MLPs in a range of critical layers read this and write memories into the residual stream
- ☐ **B.** Facts are stored only in the final softmax layer’s bias vector, which MEMIT overwrites for each new fact
- ☐ **C.** Early-layer attention gathers the subject into the last subject token
- ☐ **D.** Later attention reads these hidden states to produce the output

**Q108.** ○ *Single answer.* Which MEMIT editing criterion is about not disturbing unrelated facts?

- ○ **A.** Generalization, which checks that the new fact is recalled under many different phrasings
- ○ **B.** Specificity
- ○ **C.** Effectiveness
- ○ **D.** Fluency


### Answer key — Class 4 · Transformers

**Q84 → D**

If q and k have components with zero mean and unit variance, q·k has variance d_k. Large-magnitude logits saturate the softmax into near one-hot outputs with near-zero gradients. Vaswani et al. note that unscaled dot-product attention is outperformed by additive attention at large d_k. Dot-product attention is preferred because it is faster and more space-efficient via optimized matrix multiplication.

- A: ✗ Scaling is a constant, so it has no effect on the parameter count.
- B: ✗ The softmax already normalizes rows to sum to 1.
- C: ✗ Additive attention uses a feed-forward network. Scaling is what fixes dot-product attention at large d_k.
- D: ✓ Correct.

**Q85 → A, C, E**

The query is the representation of the current task (“what word follows ‘too’?”). Keys describe which prediction tasks each word can help with. Values are each word’s unweighted contribution. Output Z = weights · V with shape (n, d_v).

- A: ✓ Correct. This is John Hewitt’s “fuzzy key-value store” view.
- B: ✗ Roles are swapped. Values are the content that is summed; keys are matched against queries.
- C: ✓ Correct. The attention arithmetic itself has no parameters.
- D: ✗ That would be hard attention. Softmax gives a weighted average over all values.
- E: ✓ Correct.

**Q86 → C**

The original Transformer adds sinusoidal encodings PE(pos, 2i) = sin(pos / 10000^{2i/d_model}) and PE(pos, 2i+1) = cos(·) to the token embeddings. The wavelengths form a geometric progression from 2π to 10000·2π, and PE_{pos+k} is a linear function of PE_pos, which helps the model attend by relative position.

- A: ✗ That is the job of the causal mask.
- B: ✗ Positional encodings do not change memory complexity.
- C: ✓ Correct.
- D: ✗ Positional encodings are added element-wise in the same dimension. They add no extra dimensions.

**Q87 → A, B, D**

BERT-Base has L = 12, H = 768 and A = 12 heads, so each head works in a 64-dimensional subspace (768/12).

- A: ✓ Correct. Vaswani et al. visualize layer-5 heads tracking “making … more difficult” and resolving “its.”
- B: ✓ Correct.
- C: ✗ Heads have separate projections. Averaging identical heads would add nothing.
- D: ✓ Correct.

**Q88 → B**

Masking enforces the autoregressive property: p(x_t | x_<t). The model cannot peek at the future, and training is still parallel across positions because the whole masked matrix is computed in one pass.

- A: ✗ Padding masks exist, but the causal mask specifically blocks future positions.
- B: ✓ Correct.
- C: ✗ Cross-attention explicitly uses the encoder output.
- D: ✗ That is MLM masking of inputs, not attention masking.

**Q89 → A**

Cross-attention is regular dot-product attention across two sequences. Each decoder token decides which encoded input tokens are most relevant to the next prediction, which is how translation and summarization models (T5, BART) connect input meaning to output.

- A: ✓ Correct.
- B: ✗ Then the decoder state would not influence what is retrieved.
- C: ✗ That is decoder self-attention.
- D: ✗ This is reversed. The decoder asks the questions (queries).

**Q90 → B, C, D**

The lecture adds that “reality is a bit blurry”: GPT-style models can be prompted to translate, and BERT can be applied to summarization. The lecture also notes that a decoder-only model uses roughly half the parameters of a comparable encoder–decoder.

- A: ✗ Encoder-only models use unmasked (bidirectional) attention.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.

**Q91 → A, B, C, D**

The same architecture is used for pretraining and fine-tuning, and the pretrained parameters initialize every downstream task (SQuAD, SWAG, MRPC, …). A pre-trained encoder alone struggles with generation, e.g., filling “George Washington [MASK] the Delaware” only as a single-token cloze task.

- A: ✓ Correct. This is what makes deep bidirectional pretraining possible.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✗ Those are BERT-Base numbers. Large is L = 24, H = 1024, A = 16, about 340M parameters.

**Q92 → B**

Raffel et al. (2020): a unified text-to-text format means one model, one loss, and one decoding procedure for every task. For classification the model simply generates the label word.

- A: ✗ T5 is encoder–decoder and outputs text.
- B: ✓ Correct.
- C: ✗ T5 is a text model.
- D: ✗ Not T5.

**Q93 → A, B, D**

Layer norm (Ba et al., 2016) standardizes sub-layer inputs, stabilizes hidden-state dynamics, regulates scale, and speeds convergence. In the pre-LN arrangement described in the lecture (and in ViT), it is applied before multi-head attention and the feed-forward network, with residual connections around each.

- A: ✓ Correct.
- B: ✓ Correct. It does not depend on other samples in the batch.
- C: ✗ That describes batch normalization.
- D: ✓ Correct.

**Q94 → D**

Lower layers capture shallow patterns (e.g., common suffixes, n-grams); upper layers capture semantic themes. For example, “interest rates” triggers a key whose value predicts “increase” or “decrease”, and “despite the rain” predicts “we”, “they” or “the event”. Outputs are aggregated through residual connections and refined layer by layer.

- A: ✗ FFN layers hold most parameters and store factual and linguistic associations.
- B: ✗ Not equivalent.
- C: ✗ They store content associations, not position.
- D: ✓ Correct.

**Q95 → A, B, C**

Steps: set up the model; estimate total, direct and indirect effects; intervene (e.g., clamp neurons) to confirm causal roles; test significance. In LLMs this identified which MLP layers mediate factual recall, which is the basis of ROME and MEMIT.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✗ The direct effect varies the input while holding the mediator fixed.

**Q96 → A, B, D, E**

Mechanism: early-layer attention gathers the subject into the last subject token; critical MLPs read it and write memories into the residual stream; later attention reads them out. MEMIT stores new key→value associations in those MLPs, focusing on the last subject token. Examples of the problem: “Arneb is in Aquila” (wrong; it is Lepus) and “Vice President is Mike Pence” (out of date).

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✗ Avoiding full retraining is the motivation. Retraining is resource-intensive and impractical.
- D: ✓ Correct.
- E: ✓ Correct. Earlier methods handled one or a few edits.

**Q97 → B**

Local layers handle micro-context with constant memory per block; memory-compressed layers exchange global information without the full quadratic memory cost. Together they let the decoder summarize long inputs (the Wikipedia generation task).

- A: ✗ Neither is removed.
- B: ✓ Correct. The convolution has kernel 3 and stride 3; queries are unchanged.
- C: ✗ It stays attention-based.
- D: ✗ Memory-compressed attention reduces keys and values, not queries.

**Q98 → A**

RNNs multiply many Jacobians over time, so gradients usually vanish and occasionally explode. Attention filters context dynamically, retrieves only relevant parts, and avoids keeping irrelevant history.

- A: ✓ Correct.
- B: ✗ That is the RNN bottleneck attention avoids.
- C: ✗ No.
- D: ✗ Attention is O(n²) in sequence length, which is more expensive for long sequences.

**Q99 → D**

Solvers struggle to fit identity mappings with stacked nonlinear layers. Residual learning fits F(x) = H(x) − x and outputs F(x) + x, so F = 0 recovers identity. The same residual idea appears in Transformers, PixelCNN and the diffusion U-Net.

- A: ✗ Not what “degradation” means here.
- B: ✗ Training error also rises, so this is not overfitting.
- C: ✗ Not the described cause.
- D: ✓ Correct. It is an optimization problem, not overfitting.

**Q100 → D**

Additive attention computes compatibility with a small MLP. Dot-product attention computes QKᵀ, which is efficient on GPUs. Scaling by 1/√d_k fixes dot-product attention’s weakness at large d_k.

- A: ✗ It uses a single-hidden-layer feed-forward network, which has parameters.
- B: ✗ Dot-product attention is faster thanks to optimized matrix multiplication.
- C: ✗ Unscaled dot-product attention loses to additive attention at large d_k.
- D: ✓ Correct.

**Q101 → D**

GPT is semi-supervised: unsupervised language-model pretraining on a large corpus, then supervised fine-tuning. Tasks such as entailment or multiple choice are converted into token sequences with delimiter tokens, with minimal changes to the architecture.

- A: ✗ Not the GPT recipe.
- B: ✗ GPT keeps its decoder-only architecture.
- C: ✗ That would discard the pretrained knowledge.
- D: ✓ Correct.

**Q102 → B**

Pretraining on large unlabeled corpora (BooksCorpus, Wikipedia) teaches general regularities of language by predicting tokens in context. The result is a general-purpose model ready for fine-tuning.

- A: ✗ Inductive bias here means useful prior knowledge, not class imbalance.
- B: ✓ Correct.
- C: ✗ Pretraining does the opposite.
- D: ✗ Pretraining does not change the architecture.

**Q103 → A**

Multi-head attention splits d_model across heads, then concatenates them and projects with W_O, so total cost is similar to one full-width head.

- A: ✓ Correct. 768 / 12.
- B: ✗ That is BERT-Large’s hidden size.
- C: ✗ That is the full hidden size, shared across heads.
- D: ✗ That confuses heads with layers.

**Q104 → A**

This quadratic cost motivates T-DMCA (local plus memory-compressed attention), GPT-3’s sparse attention and ViT’s patching.

- A: ✓ Correct.
- B: ✗ No.
- C: ✗ Every token is compared with every other token.
- D: ✗ All n² scores are computed.

**Q105 → B, C, D**

PE(pos, 2i) = sin(pos/10000^{2i/d_model}) and PE(pos, 2i+1) = cos(…). They are added element-wise to the token embeddings.

- A: ✗ Sinusoidal encodings are fixed. Learned embeddings (BERT, ViT) are a different option.
- B: ✓ Correct. This helps the model attend by relative position.
- C: ✓ Correct.
- D: ✓ Correct.

**Q106 → A**

Total = observe output change when input varies. Direct = vary input with the mediator fixed. Indirect = the effect transmitted through the mediator.

- A: ✓ Correct.
- B: ✗ Not part of the method.
- C: ✗ That isolates the mediator’s own effect, which relates to the indirect path.
- D: ✗ That gives the total effect.

**Q107 → A, C, D**

MEMIT edits by storing new key→value vector associations in those critical MLPs, spreading each update over several layers for scale.

- A: ✓ Correct.
- B: ✗ Facts are mediated by mid-layer MLPs.
- C: ✓ Correct.
- D: ✓ Correct.

**Q108 → B**

The four criteria: effectiveness, generalization, specificity and fluency.

- A: ✗ That is paraphrase robustness.
- B: ✓ Correct.
- C: ✗ Effectiveness means the new fact wins over the old one.
- D: ✗ Fluency is about natural post-edit text.


---

## Class 5 · Autoregressive Models

**Q109.** ○ *Single answer.* How do autoregressive models differ from VAEs?

- ○ **A.** They are implicit models with no density, trained adversarially against a discriminator network
- ○ **B.** They factor p(x) as ∏ p(x_t | x_<t) and model the exact distribution, not a bound
- ○ **C.** They condition each prediction on a latent random variable
- ○ **D.** They generate the whole output in one parallel step

**Q110.** ☐ *Select all that apply.* Three ways of combining positional information with token embeddings were discussed. Which statements are correct? Select all that apply.

- ☐ **A.** Learned: trainable position embeddings, as in ViT
- ☐ **B.** The magnitude of the position vector does not matter, since attention normalizes everything
- ☐ **C.** Additive: the position vector is added element-wise; the dimension is unchanged
- ☐ **D.** Concatenation: position and token vectors are stacked, which increases the dimension

**Q111.** ☐ *Select all that apply.* In the RNN computational graph (Goodfellow et al.), which roles do U, W and V play? Select all that apply.

- ☐ **A.** V: hidden-to-output weights
- ☐ **B.** U, W and V are separate matrices at every time step, so the parameter count grows with sequence length
- ☐ **C.** U: input-to-hidden weights
- ☐ **D.** W: hidden-to-hidden recurrent weights

**Q112.** ☐ *Select all that apply.* Which statements about Backpropagation Through Time (BPTT) are correct? Select all that apply.

- ☐ **A.** BPTT avoids vanishing gradients because the gradients are summed across time steps rather than multiplied
- ☐ **B.** Because weights are shared, gradients from every time step are summed for each parameter
- ☐ **C.** The RNN is unrolled into a deep feedforward network with one layer per time step
- ☐ **D.** Loss can be computed at each step or only at the final step, depending on the task
- ☐ **E.** The gradient at time t includes terms from future time steps

**Q113.** ☐ *Select all that apply.* Which statements about LSTM gates are correct? Select all that apply.

- ☐ **A.** The forget gate sets the self-loop weight of the cell state through a sigmoid, between 0 and 1
- ☐ **B.** The output gate can shut off the cell’s output h_t
- ☐ **C.** All gates use ReLU activations, so that their outputs are unbounded and the gradients cannot saturate
- ☐ **D.** The input gate decides how much new information is written to the cell state

**Q114.** ○ *Single answer.* In a GRU, what happens when the reset gate is close to 0?

- ○ **A.** The GRU becomes an LSTM with three separate gates, gaining a dedicated output gate on the hidden state
- ○ **B.** The output h_t is forced to zero for that step, regardless of what the update gate says
- ○ **C.** The previous hidden state is copied unchanged to the next step
- ○ **D.** The candidate state ignores the previous hidden state and resets using only the current input

**Q115.** ○ *Single answer.* Luong et al. (2015) compared global and local attention for neural machine translation. Which statement is correct?

- ○ **A.** Attention reduced BLEU compared to non-attentional systems
- ○ **B.** Local attention predicts an aligned position p_t and attends to a small window around it
- ○ **C.** Global attention attends to a fixed-size window; local attention attends to all source words
- ○ **D.** Local attention always gives blurrier alignments than global attention, because a small window spreads weight more evenly

**Q116.** ☐ *Select all that apply.* PixelCNN uses masked convolutions. Which statements are correct? Select all that apply.

- ☐ **A.** Pixels are generated in raster-scan order, row by row and left to right
- ☐ **B.** The Type B mask, used in later layers, includes the center position
- ☐ **C.** Standard unmasked convolutions suffice because pixels already have a natural sequential ordering
- ☐ **D.** The Type A mask, used in the first layer, excludes the center pixel and all later pixels
- ☐ **E.** Masks are binary matrices multiplied element-wise with the filters

**Q117.** ○ *Single answer.* Why can a Type B mask include the center pixel without breaking the autoregressive property?

- ○ **A.** Because later layers are frozen during training and therefore cannot leak information about future pixels
- ○ **B.** It does break the property, but the error is small
- ○ **C.** After a Type A first layer, the center feature already depends only on earlier pixels
- ○ **D.** Because the center pixel is always zero after the first layer’s ReLU, so including it adds nothing

**Q118.** ○ *Single answer.* Using the sentence “I went to the bank to withdraw money,” what does the lecture say a self-attention head linking “bank” and “withdraw” achieves?

- ○ **A.** It establishes subject–verb agreement between “I” and “went”
- ○ **B.** It predicts the next token after “money” by attending only to the final word
- ○ **C.** It disambiguates “bank” as a financial institution
- ○ **D.** It encodes the absolute position of “bank”

**Q119.** ○ *Single answer.* In an LSTM, which component carries information across long time spans through a linear self-loop?

- ○ **A.** The cell (state) unit s_t, whose self-loop weight is set by the forget gate
- ○ **B.** The output gate, which stores the previous output h_{t−1} and feeds it back unchanged
- ○ **C.** The softmax output layer, which keeps a running average of past predictions over time
- ○ **D.** The input feature unit, which uses a ReLU so that its activations never saturate across long time spans

**Q120.** ○ *Single answer.* Why is encoding an entire past sequence into one RNN hidden vector problematic, according to the lecture?

- ○ **A.** The hidden vector cannot be updated after the first time step
- ○ **B.** The hidden vector grows linearly with the sequence length, which quickly exhausts the available GPU memory
- ○ **C.** RNNs cannot process text
- ○ **D.** A single vector is an inefficient bottleneck, and most of its context is irrelevant to the next step

**Q121.** ○ *Single answer.* A sequence-to-sequence RNN with attention translates “A B C D” into “X Y Z <eos>”. What does the <eos> token do?

- ○ **A.** It indicates an unknown word that was not in the vocabulary when the model was trained
- ○ **B.** It marks the end of the sentence so the decoder knows when to stop
- ○ **C.** It is the attention context vector
- ○ **D.** It encodes the absolute position of the last source word so that local attention can center its window

**Q122.** ○ *Single answer.* PixelCNN outputs, for each pixel, what kind of prediction?

- ○ **A.** A probability distribution over the pixel’s values given earlier pixels
- ○ **B.** A noise estimate as in diffusion
- ○ **C.** A single deterministic pixel value with no uncertainty
- ○ **D.** A latent vector for a VAE decoder, which then reconstructs the full image in one forward pass

**Q123.** ○ *Single answer.* A GRU’s update gate u_t close to 1 (in the Goodfellow formulation) means

- ○ **A.** the previous hidden state is mostly copied forward
- ○ **B.** the reset gate is disabled and the GRU behaves like a plain feed-forward layer for that step
- ○ **C.** the state is fully replaced by the new candidate
- ○ **D.** the output is zero

**Q124.** ☐ *Select all that apply.* Which are listed applications of LSTMs? Select all that apply.

- ☐ **A.** Text generation
- ☐ **B.** Computing exact image likelihoods by modeling pixels with masked convolutions in raster order
- ☐ **C.** Sentiment analysis
- ☐ **D.** Time-series forecasting
- ☐ **E.** Audio classification

**Q125.** ○ *Single answer.* In ViT, how are learned positional embeddings handled?

- ○ **A.** They are computed from pixel coordinates by a CNN
- ○ **B.** They are fixed sinusoids
- ○ **C.** They are concatenated to each patch embedding, which doubles the model width for every layer
- ○ **D.** They are trainable vectors, the same size as the patch embeddings, added to them


### Answer key — Class 5 · Autoregressive Models

**Q109 → B**

Autoregressive models turn generation into a sequential process conditioned on previous values (word by word or pixel by pixel), with explicit modeling of the data-generating distribution. VAEs instead optimize the ELBO approximation.

- A: ✗ That describes GANs.
- B: ✓ Correct. Autoregressive models belong to the tractable explicit-density family.
- C: ✗ That describes VAEs.
- D: ✗ Generation is sequential, one token or pixel at a time.

**Q110 → A, C, D**

Design criteria: positions must be distinct; magnitudes must be controlled; and the method should balance mixing information against computational complexity. Example: “Engineer” −0.9748 + position 0.1566 = −0.8182 under the additive scheme.

- A: ✓ Correct.
- B: ✗ The lecture warns that a high-magnitude position vector destroys the semantic meaning of tokens.
- C: ✓ Correct.
- D: ✓ Correct.

**Q111 → A, C, D**

h_t = tanh(b + W h_{t−1} + U x_t), o_t = c + V h_t, ŷ_t = softmax(o_t). The loss compares ŷ_t to the target y_t at each step.

- A: ✓ Correct.
- B: ✗ Parameters are shared across time steps, which is why BPTT sums their gradients.
- C: ✓ Correct.
- D: ✓ Correct.

**Q112 → B, C, D, E**

Long sequences (over 1,000 tokens) need about 1,000 matrix products forward and another 1,000 backward, which brings memory pressure and numerical instability. These are the motivations for LSTMs and attention.

- A: ✗ Summation is across occurrences of a parameter, but each term still contains a product of many Jacobians, so gradients still vanish or explode.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✓ Correct, because h_t affects all later hidden states and losses.

**Q113 → A, B, D**

The linear self-loop of the cell state, gated by the forget gate, lets gradients flow over hundreds of steps, which addresses the vanishing gradient problem (Hochreiter & Schmidhuber, 1997). Applications: time-series forecasting, sentiment analysis, audio classification, text generation.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✗ Gates use sigmoids so their values lie in (0, 1). The input unit can use any squashing nonlinearity, e.g., tanh.
- D: ✓ Correct.

**Q114 → D**

A GRU has two gates. The update gate u controls how much of the previous state carries over (it plays the roles of forget and input gate together). The reset gate r controls which parts of the past state feed into the candidate state, which lets the GRU drop information that turns out to be irrelevant.

- A: ✗ No such conversion happens.
- B: ✗ The reset gate does not zero the output.
- C: ✗ Copying is controlled by the update gate.
- D: ✓ Correct.

**Q115 → B**

Global: a variable-length alignment vector over all source states, with dot-product scoring working best. Local: monotonic or predictive variants, with the general scoring function best for predictive alignment; the context vector comes only from the window.

- A: ✗ Attention gave about +5.0 BLEU, and an ensemble reached 25.9 BLEU on WMT’15 English→German.
- B: ✓ Correct.
- C: ✗ This is reversed.
- D: ✗ Local attention gives sharper alignments with limited context; global attention tends to be blurrier.

**Q116 → A, B, D, E**

PixelCNN is trained autoregressively, using masked conv layers to enforce ordering and residual blocks (skip connections) for depth. Each pixel is conditioned only on previously generated pixels.

- A: ✓ Correct.
- B: ✓ Correct. After the first layer, the center feature already encodes only past pixels.
- C: ✗ Standard convolutions see future pixels. Masking imposes the ordering.
- D: ✓ Correct. The prediction cannot depend on the pixel’s own value.
- E: ✓ Correct.

**Q117 → C**

Information about pixel i itself enters only through the input. The Type A mask blocks it at the first layer, and every later feature at position i aggregates only from predecessors, so Type B layers can safely use the center.

- A: ✗ Later layers are trained.
- B: ✗ It does not break the property.
- C: ✓ Correct.
- D: ✗ Pixels are not zero in general.

**Q118 → C**

Multi-head analysis from the lecture: head 1 links I–went (actor); head 2 went–to the bank (destination); head 3 bank–withdraw (purpose); head 4 withdraw–money (action–object); head 5 bank–withdraw for contextual meaning. Different heads capture different relations at the same time.

- A: ✗ That is a different head’s pattern.
- B: ✗ That is not described.
- C: ✓ Correct.
- D: ✗ Positional encodings do that.

**Q119 → A**

s_t = f_t ⊙ s_{t−1} + g_t ⊙ (input feature). Because this update is additive, with a gate-controlled linear self-loop, gradients can flow across many steps when f_t ≈ 1. The gating units can also take s_{t−1} as an extra input (peephole connections).

- A: ✓ Correct.
- B: ✗ The output gate only controls how much of the cell is exposed as h_t.
- C: ✗ Not part of the recurrence.
- D: ✗ The input unit computes candidate content. It does not carry memory across time.

**Q120 → D**

The analogy: keeping every previous physical state in working memory instead of the key features. Attention instead retrieves only the relevant context on demand.

- A: ✗ It is updated at every step.
- B: ✗ The hidden vector has a fixed size. That fixed size is the problem.
- C: ✗ They can. LSTMs are used for text generation and sentiment analysis.
- D: ✓ Correct.

**Q121 → B**

Autoregressive decoders generate until they emit <eos>. This lets them produce variable-length outputs, as in Luong et al.’s stacked recurrent NMT architecture.

- A: ✗ That is usually <unk>.
- B: ✓ Correct.
- C: ✗ The context vector is computed from source states, not a token.
- D: ✗ It is a vocabulary symbol, not a positional encoding.

**Q122 → A**

Generation samples one pixel at a time from p(x_i | x_<i) in raster order, feeding each new pixel back in. This is slow but gives an exact likelihood.

- A: ✓ Correct.
- B: ✗ That is diffusion.
- C: ✗ Autoregressive models output distributions to sample from.
- D: ✗ PixelCNN has no latent variable.

**Q123 → A**

h_t = u ⊙ h_{t−1} + (1 − u) ⊙ candidate. Update gates can copy dimensions or replace them with the target state at the sigmoid extremes. Conventions differ between sources, so check which one the exam uses.

- A: ✓ Correct.
- B: ✗ The two gates act independently.
- C: ✗ In Goodfellow’s notation, u near 1 keeps the old state.
- D: ✗ Not what the gate does.

**Q124 → A, C, D, E**

Advantages: learning long-term dependencies, robustness to vanishing gradients, a flexible architecture, and wide framework support (Keras LSTM and GRU layers).

- A: ✓ Correct.
- B: ✗ That describes PixelCNN.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✓ Correct.

**Q125 → D**

Class 5 uses ViT as the example of learned positional embeddings: initialized as parameters and optimized with the rest of the model.

- A: ✗ No CNN is involved.
- B: ✗ ViT learns them.
- C: ✗ They are added, not concatenated.
- D: ✓ Correct.


---

## Class 6 · Multimodal LLMs

**Q126.** ○ *Single answer.* How does Byte Pair Encoding (BPE) build its vocabulary?

- ○ **A.** It clusters words by embedding similarity using k-means, then assigns each cluster a single shared token id
- ○ **B.** It splits text into fixed 4-character chunks and assigns each distinct chunk its own token id
- ○ **C.** It starts from single characters and repeatedly merges the most frequent adjacent pair
- ○ **D.** It assigns one token to each whole word in the training corpus

**Q127.** ☐ *Select all that apply.* Which statements about GPT-2’s adaptive input representations and adaptive softmax are correct? Select all that apply.

- ☐ **A.** Adaptive softmax clusters the vocabulary by frequency to cut the cost of the output layer
- ☐ **B.** In the 10,000-word example, the 100 most frequent words form the first cluster and are updated most often
- ☐ **C.** Adaptive softmax computes the exact full softmax over the vocabulary, only reordering words so the frequent ones are cached
- ☐ **D.** Adaptive input gives frequent words larger embeddings and rare words smaller ones

**Q128.** ☐ *Select all that apply.* Which statements about the Vision Transformer (ViT) are correct? Select all that apply.

- ☐ **A.** Images are split into fixed patches (e.g., 16×16) and linearly projected
- ☐ **B.** Layer norm comes before each block, residuals after, and the MLP has two layers with GELU
- ☐ **C.** ViT keeps CNN inductive biases such as locality and translation equivariance in every layer
- ☐ **D.** A learnable [class] token is prepended, and learnable 1-D position embeddings are added

**Q129.** ○ *Single answer.* ViT experiments compared 1-D, 2-D and relative positional embeddings. What did they find?

- ○ **A.** All three performed similarly; learned 1-D embeddings still captured 2-D structure
- ○ **B.** 2-D embeddings were essential; 1-D embeddings failed to learn any spatial structure
- ○ **C.** Relative embeddings dramatically outperformed the alternatives by more than ten points of ImageNet accuracy
- ○ **D.** Removing positional embeddings had no effect at all

**Q130.** ○ *Single answer.* Mean attention distance in ViT, measured across layers, shows which pattern?

- ○ **A.** Early layers mix local and global heads; late layers are mostly global
- ○ **B.** Distance decreases with depth, so the final layers attend only to each patch’s immediate neighbors
- ○ **C.** All heads in all layers attend only to neighboring patches
- ○ **D.** Distance is constant across layers

**Q131.** ○ *Single answer.* “QFormer” in the vision-transformer lecture (Zhang et al., 2024) refers to quadrangle attention. What does it change?

- ○ **A.** It removes self-attention entirely and uses learned geometric transforms of the image instead
- ○ **B.** It replaces patches with individual pixels so that attention windows can take any shape
- ○ **C.** It is the same module as BLIP-2’s Querying Transformer that bridges a frozen image encoder and a frozen LLM
- ○ **D.** It learns a transform that deforms fixed square windows into quadrangles fitting objects

**Q132.** ☐ *Select all that apply.* Which statements about CLIP’s training are correct? Select all that apply.

- ☐ **A.** It jointly trains an image encoder and a text encoder to predict which image and text belong together in a batch
- ☐ **B.** It uses a symmetric cross-entropy loss over cosine similarities between image and text embeddings
- ☐ **C.** It is trained to generate captions autoregressively, since generation is more compute-efficient than contrastive learning
- ☐ **D.** Its pretraining set, WIT, has about 400 million image–text pairs gathered with 500,000 queries

**Q133.** ○ *Single answer.* How does CLIP perform zero-shot classification on a new dataset?

- ○ **A.** It fine-tunes a linear head on a few labeled examples from the new dataset
- ○ **B.** It uses k-means clustering on the image embeddings
- ○ **C.** It embeds class names or descriptions with the text encoder and picks the class most similar to the image
- ○ **D.** It retrains the image encoder on the new classes, freezing the text encoder so that the label space stays fixed

**Q134.** ☐ *Select all that apply.* Which limitations and risks of CLIP did the lecture highlight? Select all that apply.

- ☐ **A.** Web-scraped training data can contain and amplify social biases
- ☐ **B.** It cannot recognize text in images at all, failing even on MNIST digits and rendered sentiment text
- ☐ **C.** It struggles with specialized tasks such as lymph-node tumor detection (PatchCamelyon)
- ☐ **D.** Flexible zero-shot classifiers could be misused, e.g., for unauthorized surveillance

**Q135.** ○ *Single answer.* DALL·E 2 consists of three parts. What is the role of the prior?

- ○ **A.** It converts the text prompt into a CLIP text embedding
- ○ **B.** It generates the final pixels, conditioned on both the text prompt and the predicted image embedding
- ○ **C.** It maps the CLIP text embedding to a predicted CLIP image embedding
- ○ **D.** It filters unsafe prompts and rewrites them before they reach the text encoder and decoder

**Q136.** ☐ *Select all that apply.* Which statements about BLIP and BLIP-2 are correct? Select all that apply.

- ☐ **A.** CapFilt generates synthetic captions and filters noisy web captions
- ☐ **B.** BLIP-2 keeps the image encoder and the LLM frozen and trains a Q-Former between them
- ☐ **C.** BLIP introduces a Multimodal mixture of Encoder–Decoder (MED) for understanding and generation tasks
- ☐ **D.** In BLIP-2, Q-Former outputs are projected and fed to the LLM as a soft visual prompt
- ☐ **E.** BLIP-2 fine-tunes every weight of the vision transformer and the LLM end-to-end, since frozen components would block gradients

**Q137.** ○ *Single answer.* Pic2Word addresses zero-shot composed image retrieval (CIR). How is its mapping network trained?

- ○ **A.** On unlabeled images, mapping each frozen CLIP image embedding to a pseudo-word token
- ○ **B.** On labeled triplets of (reference image, modification text, target image)
- ○ **C.** By fine-tuning the whole CLIP model end-to-end on a large collection of sketches, cartoons and other domains
- ○ **D.** With a GAN discriminator that judges whether the composed query looks like a real caption

**Q138.** ☐ *Select all that apply.* Which statements about ScreenAI are correct? Select all that apply.

- ☐ **A.** It reaches state of the art on UI and infographic tasks with only 5B parameters
- ☐ **B.** It combines the PaLI architecture with Pix2Struct’s flexible patching
- ☐ **C.** It is a decoder-only model that skips the vision encoder and reads raw HTML source instead of screenshots
- ☐ **D.** A textual screen schema from automatic annotation, plus LLM-generated tasks, provides pretraining data

**Q139.** ☐ *Select all that apply.* Which statements about Flamingo’s architecture are correct? Select all that apply.

- ☐ **A.** A frozen NFNet-F6 vision encoder, pretrained with a CLIP-style contrastive loss, extracts features
- ☐ **B.** The Perceiver Resampler maps variable-size visual features to a fixed set of 64 visual tokens
- ☐ **C.** Frozen LM blocks are interleaved with new GATED XATTN-DENSE cross-attention blocks
- ☐ **D.** The gates use tanh(α) with α initialized to 0, so the model starts identical to the original LM
- ☐ **E.** The language model is fully fine-tuned from scratch on interleaved image–text data so it can learn visual grounding

**Q140.** ○ *Single answer.* Why are Flamingo’s cross-attention outputs multiplied by tanh(α) with α initialized to 0?

- ○ **A.** To enforce sparsity in the attention weights, so each token attends to at most one visual token
- ○ **B.** Because tanh is required for the softmax to be stable
- ○ **C.** So the model starts out exactly like the frozen LM, for stable training
- ○ **D.** To speed up inference by skipping the vision encoder at test time

**Q141.** ☐ *Select all that apply.* Which limitations of Flamingo did the lecture list? Select all that apply.

- ☐ **A.** Its classification performance trails contrastive models optimized for image–text retrieval
- ☐ **B.** In-context learning is sensitive to demonstration quality and scales poorly beyond the low-data regime
- ☐ **C.** It inherits weaknesses of the pretrained LM, such as hallucinations and ungrounded guesses
- ☐ **D.** It cannot process video at all, because the Perceiver Resampler only accepts a single still image per sequence

**Q142.** ○ *Single answer.* A multimodal embedding model such as CLIP is valuable mainly because it

- ○ **A.** generates high-resolution images directly from text without any decoder or prior network
- ○ **B.** requires no training data, because the embeddings come from a fixed, hand-designed feature extractor
- ○ **C.** puts several modalities in one shared, directly comparable vector space
- ○ **D.** stores images and text in separate, incompatible vector spaces

**Q143.** ○ *Single answer.* Why does the Perceiver Resampler help Flamingo?

- ○ **A.** It fine-tunes the vision encoder, which would otherwise stay random because it is never pretrained
- ○ **B.** It replaces the language model
- ○ **C.** It increases the number of visual tokens for higher fidelity
- ○ **D.** It turns any number of visual features into 64 tokens, cutting cross-attention cost

**Q144.** ○ *Single answer.* How does Flamingo’s vision encoder differ from the one in the lecture’s CLIP description?

- ○ **A.** They are identical
- ○ **B.** Flamingo uses a ViT, while CLIP uses no image encoder
- ○ **C.** Flamingo trains its encoder from scratch with a captioning loss, as part of the full model
- ○ **D.** Flamingo uses a frozen NFNet-F6, trained with a CLIP-style contrastive loss

**Q145.** ☐ *Select all that apply.* Which tasks does composed image retrieval (CIR) cover in Pic2Word? Select all that apply.

- ☐ **A.** Object composition, e.g., adding or removing objects
- ☐ **B.** Attribute editing, e.g., changing color or texture
- ☐ **C.** Generating new pixels for the modified image with a diffusion decoder conditioned on the pseudo token
- ☐ **D.** Domain conversion, e.g., real photo to sketch or cartoon

**Q146.** ○ *Single answer.* Reported zero-shot CLIP robustness: by how much did it reduce the accuracy gap between ImageNet and natural-distribution-shift datasets?

- ○ **A.** By up to 75%
- ○ **B.** It widened the gap
- ○ **C.** By up to 10%
- ○ **D.** It closed the gap completely on all seven shift datasets, so it reached 100% of ImageNet accuracy

**Q147.** ○ *Single answer.* Compute for AI models other than Transformers grew by about 2× every 8 months. What is the takeaway for LLM training?

- ○ **A.** Any university lab can train GPT-3-scale models on a single GPU in a few days with standard tools
- ○ **B.** Data is no longer a constraint
- ○ **C.** Cost, data and expertise rise steeply; one GPT-3 run can cost over $12M
- ○ **D.** Compute requirements are shrinking


### Answer key — Class 6 · Multimodal LLMs

**Q126 → C**

Example: if “t”+“h” is the most frequent pair, it becomes the single symbol “th”. The process repeats thousands of times over the corpus. The final vocabulary ranges from single characters to multi-character sequences, so any string can be encoded.

- A: ✗ BPE is frequency-based merging, not clustering.
- B: ✗ Merges are data-driven, not fixed-length.
- C: ✓ Correct. Subwords like “pre” and “ing” emerge.
- D: ✗ Word-level vocabularies cannot handle unseen words. BPE builds subwords.

**Q127 → A, B, D**

Both techniques spend capacity and compute on the words that matter most, with minimal performance loss (Joulin et al., 2017). GPT-3 (175B parameters, June 2020) added sparse attention, multi-head refinements and pipeline optimizations.

- A: ✓ Correct.
- B: ✓ Correct. The next 900 form cluster 2 and the remaining 9,000 rare words form cluster 3.
- C: ✗ It is an approximation. Rare words are handled through a cluster representation at level 1.
- D: ✓ Correct.

**Q128 → A, B, D**

Hybrid alternatives apply self-attention to CNN feature maps or use local self-attention. A full Transformer over high-resolution pixels is computationally expensive, which is why ViT works on patches.

- A: ✓ Correct. Hence “An Image is Worth 16×16 Words.”
- B: ✓ Correct.
- C: ✗ ViT lacks these biases, which is a key challenge and why it needs large-scale data.
- D: ✓ Correct.

**Q129 → A**

Visualizations show 1-D embeddings assigning similar vectors to patches in the same row or column. 1-D embeddings are also the most computationally efficient, which is why they are the default.

- A: ✓ Correct.
- B: ✗ 1-D embeddings learned 2-D structure on their own.
- C: ✗ Differences were minimal.
- D: ✗ The comparison was among embedding types. Some positional information still matters.

**Q130 → A**

Mean attention distance is the average image-space distance between a query patch and the patches it attends to, weighted by attention. It is loosely analogous to the receptive field size in CNNs. Global integration in late layers supports the final prediction, and attention maps highlight semantically relevant regions.

- A: ✓ Correct.
- B: ✗ This is reversed.
- C: ✗ Some heads attend globally even in early layers.
- D: ✗ It changes systematically with depth.

**Q131 → D**

The transformation matrix is decomposed into scaling, shearing, rotation, translation and projection, which makes optimization easier. Benefits: adaptive regions, cross-window information exchange, and computational cost comparable to fixed-window ViTs. The hierarchical variant merges tokens at each stage while increasing channels.

- A: ✗ It modifies window attention. It does not remove attention.
- B: ✗ Patch tokenization is kept.
- C: ✗ This is a naming trap. BLIP-2’s Q-Former is a different model.
- D: ✓ Correct.

**Q132 → A, B, D**

Steps: embed images and texts, compute cosine similarity, then update both encoders so matching pairs score high and mismatched pairs low. In the lecture’s description, the image encoder is ResNet-based and the text encoder is a Transformer.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✗ The contrastive objective was chosen because it is more efficient than generative or autoregressive prediction.
- D: ✓ Correct. There are up to 20,000 pairs per query for balance.

**Q133 → C**

Zero-shot CLIP is competitive with a fully supervised ResNet-50 linear probe across many datasets and matches 4-shot logistic regression. It is more robust to natural distribution shift, closing the ImageNet-to-shift-set gap by up to 75%. Fine-tuning on ImageNet reduces this robustness.

- A: ✗ That is few-shot linear probing, not zero-shot.
- B: ✗ Not how CLIP classifies.
- C: ✓ Correct.
- D: ✗ No training is involved in zero-shot transfer.

**Q134 → A, C, D**

Emergent capabilities from natural-language supervision include OCR, facial emotion recognition (comparable to humans on FER2013), action recognition (UCF101, Kinetics-700) and geolocalization. Future directions include larger and better data, better benchmarks, and responsible deployment.

- A: ✓ Correct.
- B: ✗ OCR is one of CLIP’s emergent capabilities (MNIST, SST2).
- C: ✓ Correct.
- D: ✓ Correct.

**Q135 → C**

Pipeline: text encoder → prior → decoder. The lecture’s prior is an autoregressive encoder–decoder Transformer trained on CLIP text–image pairs to reproduce the CLIP image embedding from the CLIP text embedding. The paper also explores a diffusion prior. Providing the image embedding gives the decoder extra context and more accurate generations.

- A: ✗ That is the text encoder (a frozen CLIP model).
- B: ✗ That is the decoder.
- C: ✓ Correct.
- D: ✗ Not its role.

**Q136 → A, B, C, D**

BLIP-2 stage 1: representation learning, training the Q-Former on frozen ViT outputs plus captions with three contrastive-like objectives. Stage 2: generative learning, connecting to the frozen LLM through a projection layer. Earlier models handled either understanding (retrieval) or generation (captioning); BLIP unifies both.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✗ Keeping both frozen is the point. Only the Q-Former and projection are trained.

**Q137 → A**

The mapping network f_M is trained with a contrastive loss so that the text embedding of the pseudo token s* reconstructs the image embedding. At inference: encode the query image, map it to s*, insert it into a prompt such as “a sketch of *”, and retrieve by cosine similarity. Applications include attribute editing, object composition and domain conversion.

- A: ✓ Correct.
- B: ✗ Pic2Word avoids costly triplets. That is what makes it zero-shot.
- C: ✗ CLIP stays frozen. Only the lightweight mapping network is trained.
- D: ✗ No adversarial training.

**Q138 → A, B, D**

The annotation pipeline includes object detection, icon classification, OCR and image captioning. There is far more pretraining data than fine-tuning data. It achieves SOTA on MoTIF, Widget Captioning, MPDocVQA and WebSRC, leads ChartQA, DocVQA and InfographicVQA, and introduces new benchmarks (Screen Annotation, ScreenQA Short, Complex ScreenQA).

- A: ✓ Correct. It was trained at 670M, 2B and 5B.
- B: ✓ Correct.
- C: ✗ It is an encoder–decoder model with a ViT image encoder and an mT5/UL2 language encoder.
- D: ✓ Correct.

**Q139 → A, B, C, D**

Video frames are sampled at 1 FPS with learned temporal embeddings, then flattened. Image-causal masking lets each text token cross-attend only to the image immediately before it, while LM self-attention keeps dependencies on earlier images. Trained with up to 5 images, it generalizes to 32 at evaluation, and it adapts to new tasks by few-shot prompting without fine-tuning.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✗ The LM stays frozen. Only the new layers and the resampler are trained.

**Q140 → C**

The gate lets the model gradually learn how much visual information to inject, without disrupting the pretrained LM at the start of training. This idea of preserving pretrained knowledge while adding new conditioning recurs across multimodal models.

- A: ✗ The gate scales the whole residual contribution. It does not make attention sparse.
- B: ✗ Unrelated.
- C: ✓ Correct. tanh(0) = 0 means the new layers contribute nothing at first.
- D: ✗ The vision path is still used.

**Q141 → A, B, C**

These limits follow from its design choices: a frozen LM (inherited priors), a generative objective rather than a contrastive one (weaker retrieval and classification), and reliance on few-shot prompting.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✗ Flamingo processes video frames sampled at 1 FPS.

**Q142 → C**

Because images and text share one space, cosine similarity enables zero-shot classification, cross-modal retrieval and composed retrieval (Pic2Word). It can also be reused as the text encoder in DALL·E 2.

- A: ✗ CLIP is an embedding model, not a generator.
- B: ✗ It requires about 400M pairs.
- C: ✓ Correct.
- D: ✗ The point is a shared space.

**Q143 → D**

Learned latent queries cross-attend to the visual features. Ablations show it beats plain Transformer and MLP alternatives.

- A: ✗ The vision encoder is pretrained and frozen.
- B: ✗ The LM stays.
- C: ✗ It reduces them to a fixed number.
- D: ✓ Correct.

**Q144 → D**

The slides contrast NFNet-F6 with the ViT used in some CLIP models. The encoder’s 2-D grid is flattened before the resampler.

- A: ✗ Different architectures.
- B: ✗ Both have image encoders.
- C: ✗ Its encoder is pretrained contrastively and then frozen.
- D: ✓ Correct.

**Q145 → A, B, D**

The query is an image plus a text modification. Strengths: zero-shot generalization, cost-effectiveness, flexibility, scalability and interpretability (images become pseudo-words).

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✗ CIR retrieves existing images from a database. It does not generate.
- D: ✓ Correct.

**Q146 → A**

The seven shift datasets vary pose, background and renditions. Fine-tuning CLIP on ImageNet reduces this robustness.

- A: ✓ Correct.
- B: ✗ It narrowed it.
- C: ✗ Too small.
- D: ✗ Not completely.

**Q147 → C**

The critical factors listed: compute and cost, scale of data, and the technical expertise for distributed systems and GPU management.

- A: ✗ It takes thousands of GPUs and months.
- B: ✗ Private-domain data is scarce.
- C: ✓ Correct.
- D: ✗ They are growing rapidly.


---

## Class 7 · Diffusion Models

**Q148.** ☐ *Select all that apply.* Which statements describe diffusion models as presented in Prince (2023) and Ho et al. (2020)? Select all that apply.

- ☐ **A.** Like VAEs, they are trained by maximizing a lower bound (ELBO) on the likelihood
- ☐ **B.** All learned parameters live in the decoder (reverse process)
- ☐ **C.** The forward process is learned jointly with the decoder, as the encoder of a VAE is
- ☐ **D.** The forward process is fixed and gradually blends data with noise
- ☐ **E.** The latent variables z₁…z_T have the same dimensions as the data x

**Q149.** ○ *Single answer.* The forward process is z_t = √(1 − β_t) · z_{t−1} + √β_t · ε_t. What do the two terms do?

- ○ **A.** The first adds noise and the second removes it
- ○ **B.** The first rotates the data and the second rescales it so that the total norm stays unchanged
- ○ **C.** The first attenuates the current signal; the second adds fresh Gaussian noise
- ○ **D.** Both terms add noise, while β_t is learned by backpropagation so that the forward process can adapt to the data

**Q150.** ○ *Single answer.* What is the diffusion kernel q(z_t | x), and why is it useful?

- ○ **A.** The learned reverse distribution, which must be computed by running all t intermediate steps sequentially
- ○ **B.** A small neural network trained alongside the decoder to predict z_t from x at each step
- ○ **C.** A uniform distribution over noise levels, used to choose which timestep each training example gets
- ○ **D.** A closed-form Gaussian N(√α_t · x, (1 − α_t) I) with α_t = ∏(1 − β_s); it samples z_t in one step

**Q151.** ☐ *Select all that apply.* Reverse conditionals in diffusion models. Which statements are correct? Select all that apply.

- ☐ **A.** Each reverse step is approximated by a Gaussian with a network mean and fixed variance
- ☐ **B.** q(z_{t−1} | z_t) is generally intractable, because it requires the complex marginal q(z_{t−1})
- ☐ **C.** The normal approximation to the reverse step is reasonable only when β_t is large and T is small
- ☐ **D.** q(z_{t−1} | z_t, x), conditioned on the original data, is Gaussian with a closed form

**Q152.** ○ *Single answer.* Ho et al. reparameterized the training target. Instead of predicting z_{t−1}, the network predicts

- ○ **A.** the noise ε that was added, giving a simpler loss that works better
- ○ **B.** the noise schedule β_t, which the network learns to set separately for each training image and each step
- ○ **C.** the class label of the image
- ○ **D.** the original image x directly, in a single step from any z_t

**Q153.** ☐ *Select all that apply.* Which statements about the U-Net used in diffusion models are correct? Select all that apply.

- ☐ **A.** A separate U-Net is trained for every one of the T = 1,000 timesteps, with no time embedding
- ☐ **B.** It is used because its output has the same shape as its input, matching the predicted noise
- ☐ **C.** Downsampling cuts spatial size and adds channels; upsampling reverses it
- ☐ **D.** Encoder features are concatenated to matching decoder stages through skip connections
- ☐ **E.** A single network serves all time steps, given a sinusoidal time (noise-level) embedding

**Q154.** ○ *Single answer.* In Ho et al. (2020), what noise schedule was used, and what did later work find?

- ○ **A.** β_t linear from 0.0001 to 0.02; a later paper found a cosine schedule worked better
- ○ **B.** β_t decreasing from 0.02 down to 0.0001, so that the largest noise steps happen first; later work kept this unchanged
- ○ **C.** A learned schedule from the start
- ○ **D.** A constant β = 0.5 for all steps; later work found a linear schedule better

**Q155.** ☐ *Select all that apply.* Foster’s sampler takes 20 steps, although training used 1,000 noise levels. Which statements are correct? Select all that apply.

- ☐ **A.** With σ_t = 0 at every step (DDIM), the same input noise always yields the same output
- ☐ **B.** The number of sampling steps can be far smaller than the number of training steps
- ☐ **C.** Sampling must run exactly 1,000 steps, because the U-Net only knows the noise levels it saw during training
- ☐ **D.** Each step predicts the noise, estimates x₀, then re-noises that estimate to the t − 1 level

**Q156.** ○ *Single answer.* Why is spherical interpolation, rather than plain linear interpolation, used between two Gaussian noise tensors a and b?

- ○ **A.** Spherical interpolation removes the need to run the reverse denoising process for the in-between images
- ○ **B.** It produces images from different classes, which helps cover the whole data distribution
- ○ **C.** It keeps the noise variance constant, so every interpolant still looks like N(0, I) noise
- ○ **D.** Linear interpolation is not differentiable

**Q157.** ☐ *Select all that apply.* Two approaches to conditional generation were described. Which statements are correct? Select all that apply.

- ☐ **A.** Both approaches require retraining a separate diffusion model for each class that needs to be generated
- ☐ **B.** Classifier guidance adds a classifier gradient term to steer toward class c
- ☐ **C.** Classifier-free guidance embeds the class in the U-Net, trained with and without it
- ☐ **D.** Classifier-free guidance allows a continuous quality–diversity trade-off by weighting the conditioning

**Q158.** ○ *Single answer.* How does the diffusion training procedure sketched in the lecture handle the intractable likelihood P(x) = ∫ P(x, z₁…z_T) dz?

- ○ **A.** It ignores the likelihood and uses only perceptual loss
- ○ **B.** It lower-bounds the log-likelihood with Jensen’s inequality and maximizes the ELBO
- ○ **C.** It replaces the likelihood with an adversarial loss from a discriminator that tells real images from denoised ones
- ○ **D.** It computes the integral exactly with Monte Carlo over all paths

**Q159.** ☐ *Select all that apply.* Which statements about Sora (“Video generation models as world simulators”) are correct? Select all that apply.

- ☐ **A.** It reliably models physics, such as glass shattering, and correctly updates object state after actions like eating
- ☐ **B.** Videos are compressed into a latent space and cut into spacetime patches that act as transformer tokens
- ☐ **C.** Emergent abilities include 3D consistency and long-range coherence (object permanence)
- ☐ **D.** It is a diffusion transformer that predicts clean patches from noisy ones, conditioned on text
- ☐ **E.** It trains on native resolutions, durations and aspect ratios instead of cropping to a fixed size

**Q160.** ○ *Single answer.* Prince’s “Catty10 → Catty9” analogy illustrates which part of diffusion training?

- ○ **A.** Computing the marginal distribution q(z_t)
- ○ **B.** Learning each reverse step: from a t-step-noised image, predict the (t−1)-step version
- ○ **C.** Training a discriminator that distinguishes scribbled copies from clean originals, as in adversarial training
- ○ **D.** Training the forward process to add the right amount of noise for each individual image

**Q161.** ○ *Single answer.* What does the marginal q(z_t) represent?

- ○ **A.** The distribution of z_t over all starting data points and all diffusion paths
- ○ **B.** The distribution of one particular training image after it has been noised for t steps
- ○ **C.** A delta function at zero, since every diffusion path eventually reaches the origin
- ○ **D.** The learned reverse distribution produced by the U-Net at step t, after training has converged on the data

**Q162.** ○ *Single answer.* With T = 100 and β = 0.03 at every step, what happens to three different 1-D starting values x as they pass through z₁…z₁₀₀?

- ○ **A.** They stay exactly at their starting values, because the noise added at each step has a mean of exactly zero
- ○ **B.** They move apart without bound because noise accumulates
- ○ **C.** They drift noisily toward zero, and their paths become indistinguishable from N(0, 1)
- ○ **D.** They converge to the mean of the data distribution

**Q163.** ☐ *Select all that apply.* Which statements about generating a sample from a trained diffusion model are correct? Select all that apply.

- ☐ **A.** Repeatedly sample z_{t−1} from N(f_t[z_t, φ_t], σ_t² I) down to x (ancestral sampling)
- ☐ **B.** Start by drawing z_T from a standard normal
- ☐ **C.** Generation is iterative and therefore slower than a single VAE or GAN decoder pass
- ☐ **D.** Start from a real training image and add noise until it matches the target class
- ☐ **E.** The forward noising process must be run first on a training image to produce the starting latent

**Q164.** ○ *Single answer.* With a linear schedule β from 0.0001 to 0.02 over T = 1,000 steps, why are early steps small?

- ○ **A.** Early steps destroy little detail; bigger steps are fine once the image is noisy
- ○ **B.** To save memory
- ○ **C.** To make the forward process learnable
- ○ **D.** Because the U-Net is only trained on the first 10 steps, so later steps never need a gradient signal

**Q165.** ○ *Single answer.* In a DDIM step, which estimate is computed first from the network’s noise prediction ε̂?

- ○ **A.** The class label of the image, so that the sampler can pick the right noise schedule for it
- ○ **B.** The KL divergence
- ○ **C.** The predicted clean image x̂₀ = (x_t − √(1−ᾱ_t) ε̂) / √ᾱ_t
- ○ **D.** The next noise sample to add

**Q166.** ☐ *Select all that apply.* Which training setup did Foster’s Keras diffusion model use? Select all that apply.

- ☐ **A.** Normalization statistics computed on the training set
- ☐ **B.** A mean absolute error loss on the predicted noise
- ☐ **C.** A discriminator network trained jointly with the U-Net to sharpen the generated samples
- ☐ **D.** The AdamW optimizer, which is Adam with decoupled weight decay

**Q167.** ○ *Single answer.* How does the cascaded text-to-image diffusion system reach 1024×1024 output?

- ○ **A.** By tiling 256 separate 64×64 images
- ○ **B.** A GAN upsamples the 64×64 output, after the diffusion model has fixed the overall composition
- ○ **C.** 64×64 base, then 256 and 1024 stages, each conditioned on text and the smaller image
- ○ **D.** One U-Net directly generates 1024×1024

**Q168.** ○ *Single answer.* How does Sora generate images up to 2048×2048?

- ○ **A.** By upscaling with a CNN
- ○ **B.** With a separate image-only diffusion model
- ○ **C.** By generating a long video and averaging every frame into one still picture at the end
- ○ **D.** By arranging noise patches in a spatial grid one frame long


### Answer key — Class 7 · Diffusion Models

**Q148 → A, B, D, E**

Diffusion models are easy to train and produce samples that can exceed GAN realism. Generation draws z_T from N(0, I) and passes it through the learned decoder step by step.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✗ The forward process has no learned parameters. Its noise schedule is a hyperparameter.
- D: ✓ Correct.
- E: ✓ Correct. This differs from VAEs, whose latent is lower-dimensional.

**Q149 → C**

The forward process is a Markov chain: q(z_t | z_{t−1}) = N(√(1 − β_t) z_{t−1}, β_t I). If z_{t−1} has unit variance, Var(z_t) = (1 − β_t) + β_t = 1, so variance is preserved while signal is replaced by noise. After enough steps, q(z_T | x) ≈ N(0, I).

- A: ✗ Neither term removes noise.
- B: ✗ Not rotation.
- C: ✓ Correct.
- D: ✗ β_t is a fixed noise schedule, not learned.

**Q150 → D**

As t grows, the mean √α_t x shrinks toward zero and the variance 1 − α_t grows toward 1, so the kernel approaches a standard normal. Training uses it to jump directly to any noise level for a training image, the same reparameterization idea as a VAE: z_t = √α_t x + √(1 − α_t) ε.

- A: ✗ The kernel is the forward shortcut that avoids running the intermediate steps.
- B: ✗ It is an analytic distribution, not a network.
- C: ✗ It is Gaussian.
- D: ✓ Correct.

**Q151 → A, B, D**

By Bayes’ rule, q(z_{t−1} | z_t) ∝ q(z_t | z_{t−1}) q(z_{t−1}). This is often well approximated by a normal distribution, but not always. Conditioning on x makes every factor Gaussian, so the training target is exact.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✗ It is reasonable when β_t is small (close to 0) and T is large.
- D: ✓ Correct. Its mean blends z_t and x.

**Q152 → A**

The loss becomes a least-squares error between the true and predicted noise (Foster’s implementation uses mean absolute error with AdamW). Predicting the noise is an easier learning task, and the noise has the same shape as the image, which is why a U-Net is used.

- A: ✓ Correct. The loss compares ε̂ = g_t(z_t, φ) with the true ε.
- B: ✗ β_t is fixed.
- C: ✗ Unconditional DDPMs do not predict labels.
- D: ✗ Predicting the clean image is possible, but it is not the DDPM reparameterization.

**Q153 → B, C, D, E**

Residual blocks connect adjacent representations, with periodic global self-attention. In Foster’s Keras version, each DownBlock has two residual blocks and average pooling, and each UpBlock has bilinear upsampling, concatenation of skips, and two residual blocks.

- A: ✗ One shared network is conditioned on t. Prince’s cat analogy, with one network per step, is only conceptual.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✓ Correct.

**Q154 → A**

Increasing β_t means early steps destroy little detail. Nichol & Dhariwal’s cosine schedule spreads signal destruction more evenly. In terms of ᾱ_t, √ᾱ_t is the signal rate and √(1 − ᾱ_t) is the noise rate.

- A: ✓ Correct.
- B: ✗ The schedule increases: small steps early, larger ones once the image is already noisy.
- C: ✗ The DDPM schedule was fixed and linear.
- D: ✗ Neither part is right.

**Q155 → A, B, D**

Song et al. (2020) DDIM equation: x_{t−1} = √ᾱ_{t−1} · x̂₀ + √(1 − ᾱ_{t−1} − σ_t²) · ε̂ + σ_t ε. A deterministic mapping gives a well-defined correspondence between latent noise and images, which is useful for interpolation.

- A: ✓ Correct. DDIM sampling is deterministic.
- B: ✓ Correct.
- C: ✗ The time embedding is continuous, and DDIM-style updates allow skipping levels.
- D: ✓ Correct. This is the two-step jump from x_t to x_{t−1}.

**Q156 → C**

A linear midpoint (a + b)/2 of independent standard normals has variance 0.5, which is off-distribution for the denoiser. The sin/cos weights satisfy sin² + cos² = 1, preserving unit variance. With deterministic DDIM sampling this gives smooth image transitions.

- A: ✗ Every interpolant still has to be denoised by the model.
- B: ✗ Not its purpose.
- C: ✓ Correct. For example, sin(πt/2)·a + cos(πt/2)·b.
- D: ✗ It is differentiable.

**Q157 → B, C, D**

Text-to-image systems (e.g., Imagen, Saharia et al. 2022) condition on a sentence embedding from a large language model and use a cascade: 64×64 base → 256×256 → 1024×1024 super-resolution, each stage conditioned on the text and the lower-resolution image.

- A: ✗ One model handles all classes in both approaches.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.

**Q158 → B**

The loss has a reconstruction term (recovering x from z₁) and diffusion terms (matching each predicted z_{t−1} to the Gaussian target from q(z_{t−1} | z_t, x)). It is summed over data points and steps. In practice: sample a time step, diffuse with the kernel, and update the decoder.

- A: ✗ Training is likelihood-based.
- B: ✓ Correct.
- C: ✗ Diffusion models are not adversarial.
- D: ✗ The integral cannot be computed exactly.

**Q159 → B, C, D, E**

Sample quality improves markedly with compute (base → 4× → 32×). GPT expands short prompts into detailed captions. Sora animates images, extends videos, loops, does SDEdit-based editing and interpolation, and generates images up to 2048×2048 using a one-frame spatial grid.

- A: ✗ These are listed limitations. Physics and object-state changes are often wrong.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✓ Correct.

**Q160 → B**

The analogy: Net10 learns to turn 10-second scribbles into 9-second scribbles, then Net9, and so on. Generation starts from a fully scribbled image and applies the networks in reverse. In practice, one U-Net conditioned on t replaces the separate networks.

- A: ✗ The marginal is a separate idea (the overall distribution of scribbled photos).
- B: ✓ Correct.
- C: ✗ No discriminator is involved.
- D: ✗ The forward process (scribbling) is fixed. Only denoising is learned.

**Q161 → A**

q(z_t) = ∫ q(z_t | x) Pr(x) dx. Prince’s analogy: “the overall distribution of scribbled photos after scribbling for time t.” As t grows it blurs Pr(x) toward N(0, I). In a fitted model, the estimated marginals closely match these true marginals.

- A: ✓ Correct.
- B: ✗ That is the kernel q(z_t | x).
- C: ✗ It is a broad distribution.
- D: ✗ That is the model’s estimate, p(z_t).

**Q162 → C**

Each step multiplies by √0.97 ≈ 0.985 and adds noise with variance 0.03. The conditionals q(z_t | z_{t−1}) are normal, with a mean slightly closer to zero than the current point and fixed variance β_t.

- A: ✗ Zero-mean noise still spreads the values, and attenuation shrinks the mean toward zero.
- B: ✗ Attenuation by √(1 − β) keeps the variance bounded.
- C: ✓ Correct.
- D: ✗ They converge to the standard normal, centered at 0, not to the data mean.

**Q163 → A, B, C**

Speed-ups covered in the lecture: deterministic formulations (DDIM) and fewer steps (e.g., 20). Conditioning (class, image, text) can be added at every denoising step.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✗ That is closer to SDEdit-style editing. Unconditional generation starts from pure noise.
- E: ✗ Generation does not need any training image. z_T comes straight from the prior.

**Q164 → A**

A cosine schedule later improved on this by spreading the destruction of signal more evenly.

- A: ✓ Correct.
- B: ✗ Not the reason.
- C: ✗ It is fixed.
- D: ✗ All timesteps are trained.

**Q165 → C**

Then x_{t−1} = √ᾱ_{t−1} x̂₀ + √(1 − ᾱ_{t−1}) ε̂ (when σ = 0): the signal is rescaled to the t−1 rate and the predicted noise reapplied at the t−1 noise rate.

- A: ✗ No labels are involved.
- B: ✗ Not computed during sampling.
- C: ✓ Correct.
- D: ✗ Fresh noise is only added when σ_t > 0.

**Q166 → A, B, D**

The model was trained for 50 epochs. DownBlocks use average pooling; UpBlocks use bilinear upsampling plus concatenated skips.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✗ No discriminator is used.
- D: ✓ Correct.

**Q167 → C**

The text is encoded by a large language model (Saharia et al., 2022). The stochastic model yields many compatible images and can count objects and render text.

- A: ✗ Not tiling.
- B: ✗ All stages are diffusion models.
- C: ✓ Correct.
- D: ✗ It uses a cascade.

**Q168 → D**

Video size is controlled at inference by arranging randomly initialized patches in a grid of the right size. Images are simply one-frame videos.

- A: ✗ Not described.
- B: ✗ The same model is used.
- C: ✗ Not how it works.
- D: ✓ Correct.


---

## Cross-topic synthesis

**Q169.** ☐ *Select all that apply.* Skip or residual connections appear throughout the course. In which models do they play a central role? Select all that apply.

- ☐ **A.** The Transformer (around attention and FFN sub-layers)
- ☐ **B.** The diffusion U-Net
- ☐ **C.** ResNet
- ☐ **D.** The original single-layer perceptron, where the skip lets the input bypass its one weighted sum
- ☐ **E.** PixelCNN residual blocks

**Q170.** ○ *Single answer.* Which comparison of latent dimensionality is correct?

- ○ **A.** Autoregressive models such as PixelCNN use a 200-dimensional latent
- ○ **B.** Diffusion latents are lower-dimensional than the data, while VAE latents are larger than the input image
- ○ **C.** Both VAEs and diffusion models compress to a lower-dimensional latent
- ○ **D.** VAE latents are usually lower-dimensional than x; diffusion latents z₁…z_T match x’s size

**Q171.** ☐ *Select all that apply.* Masking appears in several architectures. Which statements are correct? Select all that apply.

- ☐ **A.** Flamingo masks cross-attention so each text token sees only the image just before it
- ☐ **B.** CLIP masks half of each image’s patches and trains the encoder to reconstruct the missing pixels
- ☐ **C.** BERT masks input tokens and predicts them from both sides (MLM)
- ☐ **D.** PixelCNN masks convolution weights so each pixel sees only earlier pixels in raster order
- ☐ **E.** Decoder self-attention masks future positions to keep generation autoregressive

**Q172.** ☐ *Select all that apply.* Contrastive objectives appear in several models. Which use a contrastive loss as a core training signal? Select all that apply.

- ☐ **A.** DDPM noise prediction, which contrasts each predicted noise vector against the noise of other images in the batch
- ☐ **B.** Pic2Word’s mapping network
- ☐ **C.** SimCLR
- ☐ **D.** CLIP
- ☐ **E.** Flamingo’s vision encoder pretraining

**Q173.** ○ *Single answer.* Which family generally needs one network pass per generated element, making sampling inherently sequential and slow for long outputs?

- ○ **A.** GANs, since the generator must be run once for each pixel that it outputs
- ○ **B.** Contrastive encoders like SimCLR
- ○ **C.** VAEs
- ○ **D.** Autoregressive models such as PixelCNN and GPT

**Q174.** ○ *Single answer.* Which statement correctly contrasts the role of the KL term in a VAE with the role of KL inside the diffusion ELBO?

- ○ **A.** Both regularize a learned encoder toward N(0, I)
- ○ **B.** VAE KL regularizes the learned encoder; diffusion KLs fit reverse steps to fixed targets
- ○ **C.** VAEs have no KL term; their loss is reconstruction only, while diffusion models add a KL for stability
- ○ **D.** Diffusion models have no KL terms at all; their loss is purely adversarial, comparing generated and real images

**Q175.** ○ *Single answer.* A researcher wants a model that can directly score how likely a new image is, with an exact (not bounded) log-likelihood. Which family from the course fits best?

- ○ **A.** Autoregressive model (e.g., PixelCNN)
- ○ **B.** Diffusion model
- ○ **C.** GAN
- ○ **D.** VAE, because its ELBO is always exactly equal to log p(x) once training has fully converged

**Q176.** ○ *Single answer.* Which pairing of model and generation step count is correct?

- ○ **A.** VAE: T denoising steps
- ○ **B.** GAN: one network pass per pixel, so a 64×64 image needs 4,096 sequential passes
- ○ **C.** PixelCNN: one pass for the whole image
- ○ **D.** DDPM: about 1,000 steps; DDIM: far fewer (e.g., 20)

**Q177.** ☐ *Select all that apply.* Which models freeze a large pretrained component and train only new connecting modules? Select all that apply.

- ☐ **A.** BLIP-2 (frozen image encoder and LLM; trains the Q-Former)
- ☐ **B.** Pic2Word (frozen CLIP; trains the mapping network)
- ☐ **C.** Flamingo (frozen NFNet and LM; trains the resampler and gated cross-attention)
- ☐ **D.** SimCLR, which freezes a supervised ImageNet encoder and only trains its projection head

**Q178.** ○ *Single answer.* What do the VAE, diffusion and Sora pipelines have in common regarding Gaussian noise?

- ○ **A.** They all use adversarial noise
- ○ **B.** Each samples standard-normal noise and maps it to data with a learned network
- ○ **C.** None use Gaussian noise
- ○ **D.** All three add noise only at training time and generate fully deterministically from fixed inputs


### Answer key — Cross-topic synthesis

**Q169 → A, B, C, E**

Skip connections ease optimization by representing identity mappings easily, mitigate vanishing gradients and degradation, and smooth the loss landscape. In U-Nets they also carry high-resolution detail from the encoder to the decoder by concatenation, not addition.

- A: ✓ Correct. They form the residual stream that MEMIT edits.
- B: ✓ Correct. There are residual blocks plus encoder–decoder skip concatenations.
- C: ✓ Correct. f(x) = C(x) + x.
- D: ✗ A single-layer perceptron has nothing to skip.
- E: ✓ Correct.

**Q170 → D**

A VAE compresses (2-D for Fashion-MNIST, 200-D for CelebA). Diffusion corrupts at full resolution, which is why generation is costly. Latent diffusion approaches, including Sora’s compressed spacetime latent, run diffusion in a learned compressed space.

- A: ✗ Autoregressive models have no latent variable; they condition on previous outputs.
- B: ✗ This is reversed.
- C: ✗ Diffusion latents keep the data dimension.
- D: ✓ Correct.

**Q171 → A, C, D, E**

Masking controls information flow. Causal masks (GPT, PixelCNN) enforce an ordering. Input masks (BERT) define a self-supervised objective. Cross-modal masks (Flamingo) control which media each token can see.

- A: ✓ Correct. This is image-causal masking.
- B: ✗ That describes masked autoencoders (MAE). CLIP is contrastive and has no reconstruction.
- C: ✓ Correct.
- D: ✓ Correct.
- E: ✓ Correct.

**Q172 → B, C, D, E**

Contrastive learning pulls positive pairs together and pushes negatives apart in an embedding space. A recurring theme: large batches or many negatives help, temperature matters, and the learned embeddings transfer well (zero-shot or linear probe).

- A: ✗ DDPM uses a per-sample regression (least-squares) loss.
- B: ✓ Correct (pseudo-token embedding versus image embedding).
- C: ✓ Correct (NT-Xent over augmented views).
- D: ✓ Correct (symmetric cross-entropy over image–text pairs).
- E: ✓ Correct (NFNet-F6 trained with a CLIP-style two-term loss).

**Q173 → D**

Sampling cost: autoregressive models take one pass per token or pixel; diffusion models take one pass per denoising step (1,000 in DDPM, about 20 with DDIM-style samplers); VAEs and GANs take a single pass. Training of autoregressive Transformers is still parallel thanks to causal masking.

- A: ✗ A GAN generator produces the whole image in one pass.
- B: ✗ These are not generators.
- C: ✗ A VAE generates with one decoder pass after sampling z.
- D: ✓ Correct.

**Q174 → B**

Both maximize an ELBO. In the VAE, both the encoder and decoder are learned. In diffusion, the encoder is fixed, so the KL terms only train the decoder to invert known Gaussian corruption steps.

- A: ✗ Diffusion has no learned encoder.
- B: ✓ Correct.
- C: ✗ The KL is half of the VAE loss.
- D: ✗ The ELBO decomposes into KL and reconstruction terms, which simplify to a noise-prediction MSE.

**Q175 → A**

This follows the Class 1 taxonomy: tractable explicit models (autoregressive, normalizing flows) give exact densities; approximate models (VAE, diffusion, EBM) give bounds or approximations; implicit models (GAN) give none.

- A: ✓ Correct. p(x) = ∏ p(x_i | x_<i) is computed exactly.
- B: ✗ Standard DDPM training also gives a bound, not the exact likelihood.
- C: ✗ GANs are implicit models and give no likelihood.
- D: ✗ The ELBO equals log p(x) only if q matches the true posterior exactly, which rarely happens.

**Q176 → D**

Speed is a key trade-off between the families: single-pass (VAE, GAN), iterative (diffusion) and sequential per element (autoregressive).

- A: ✗ A VAE needs one decoder pass.
- B: ✗ That is how an autoregressive model generates.
- C: ✗ PixelCNN needs one pass per pixel.
- D: ✓ Correct.

**Q177 → A, B, C**

Freezing keeps pretrained knowledge, cuts compute, and avoids catastrophic forgetting. This is the same principle as transfer learning in Class 2.

- A: ✓ Correct.
- B: ✓ Correct.
- C: ✓ Correct.
- D: ✗ SimCLR trains the encoder from scratch without labels.

**Q178 → B**

VAE: z ~ N(0, I) → decoder. Diffusion: z_T ~ N(0, I) → iterative denoiser. Sora: noisy spacetime latent patches → diffusion transformer.

- A: ✗ No.
- B: ✓ Correct.
- C: ✗ All three do.
- D: ✗ VAEs and DDPMs sample noise at generation time.

