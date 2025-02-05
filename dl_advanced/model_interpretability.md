# Model Interpretability

## Categories of Interpretability
### Intrinsic vs. Post-hoc Interpretability

- **Intrinsic Interpretability**:
Models are designed to be interpretable from the start. Examples include models with built-in attention mechanisms or architectures that incorporate human-understandable concepts (e.g., case-based reasoning models).

- **Post-hoc Interpretability**:
Interpretability methods applied after model training. These methods try to explain predictions of otherwise “black-box” models without altering the original architecture.

### Local vs. Global Explanations

- **Local Explanations**:
Focus on explaining individual predictions. Methods provide insight into why the model made a particular decision for a single instance.

- **Global Explanations**:
Aim to explain the overall behavior of the model. This involves summarizing general patterns, decision rules, or feature contributions that hold across the dataset.

### Model-specific vs. Model-agnostic Methods

- **Model-specific**:
Tailored to specific architectures (e.g., convolutional neural networks) and can leverage internal structure (like gradients, activations).
    - See `CNN interpretablity` in `../cv/cnn.md`.
    - See `Transformer visualization` in `../transformer/README.md`.
- **Model-agnostic**:
Can be applied to any predictive model. They treat the model as a black box and use input–output behavior to infer explanations.

## Popular Methodologies (Genres) and Their Representative Works

### Gradient-based Methods:
These methods use gradients or derivative information to assess the influence of input features.

Representative Works:
- Saliency Maps: Visualize the gradient of the output with respect to input pixels.
- Integrated Gradients (Sundararajan et al., 2017): Accumulate gradients along the path from a baseline input to the actual input to provide attribution scores.
- Grad-CAM (Selvaraju et al., 2017): Uses gradients flowing into the last convolutional layer of a CNN to produce coarse localization maps.

### Perturbation-based Methods:
These approaches systematically modify or occlude parts of the input to observe changes in the output.

Representative Works:
- LIME (Local Interpretable Model-agnostic Explanations, Ribeiro et al., 2016): Approximates the model locally with an interpretable surrogate (often a linear model) by perturbing the input.
- SHAP (SHapley Additive exPlanations): Uses Shapley values from cooperative game theory to fairly distribute the prediction among input features.