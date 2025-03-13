# Structured Knowledge Accumulation (SKA) Model for the Iris Dataset

## Overview
This project implements the Structured Knowledge Accumulation (SKA) model, a backpropagation-free learning framework that optimizes neural networks using layer-wise entropy reduction. Instead of propagating errors backward, SKA updates weights based on knowledge alignment with decision probability shifts.

We apply SKA to the Iris dataset and compare its performance with that of a traditional neural network trained using backpropagation (SGD, Adam). To assess SKA's effectiveness, the project analyzes convergence speed, entropy reduction trends, and classification accuracy.

## Performance Comparison

Here’s how the models performed on the Iris dataset:

1. Original SKA Model:
  - Accuracy: 36.67%
  - Training Method: Forward-only updates driven by entropy reduction, without backpropagation.
  - Details: The original SKA model struggled to achieve high accuracy, indicating that its unsupervised, entropy-driven approach alone was insufficient for this classification task.

2. SKA Model with Backpropagation:
  - Accuracy: 100%
  - Training Method: Hybrid approach combining SKA’s entropy-driven updates with supervised backpropagation.
  - Details: Adding backpropagation enabled the SKA model to match the performance of the SimpleNN, suggesting that supervised guidance significantly enhances its effectiveness.

3. Traditional Neural Network (SimpleNN):
  - Accuracy: 100%
  - Training Method: Supervised learning with backpropagation and cross-entropy loss.
  - Details: The SimpleNN quickly achieved perfect accuracy, leveraging the small size (150 samples) and simplicity of the Iris dataset (three classes, four features).

Key Takeaway: While the original SKA model underperformed with 36.67% accuracy, integrating backpropagation allowed it to reach 100% accuracy, matching the traditional neural network. This highlights the critical role of supervision for classification tasks on structured datasets like Iris.

## Convergence Analysis: Forward Steps (K) Needed

1. Original SKA Model:
- Steps: Trained for 1000 forward steps.
- Convergence: Did not fully converge, as accuracy plateaued at 36.67% despite ongoing entropy reduction. More steps might improve performance slightly, but the lack of supervised guidance limits its effectiveness.
- Observation: The model requires a large number of steps without guaranteeing high accuracy.

2. SKA Model with Backpropagation:
- Steps: Converged to 100% accuracy in fewer steps than the original SKA (exact number depends on implementation, but significantly less than 1000).
- Convergence: The supervised updates accelerated convergence by aligning the model’s internal representations with the classification task.
- Observation: Backpropagation dramatically reduces the steps needed for convergence.

3. Traditional Neural Network (SimpleNN):
- Steps: Typically converges within 10-50 epochs (depending on learning rate and batch size), equivalent to a small number of forward-backward passes.
- Convergence: Rapid convergence due to the dataset’s simplicity and the efficiency of backpropagation.
- Observation: Supervised training ensures fast and reliable convergence.

Key Takeaway: The original SKA model requires many forward steps (K=1000) without achieving high accuracy, while both the hybrid SKA and SimpleNN converge much faster with supervision, making them more efficient for this task.

## Correlation Between Entropy Reduction and Classification Accuracy

Entropy reduction is central to SKA’s learning process, but its impact on accuracy varies:

1. Original SKA Model:
- Entropy Reduction: Significant reduction in entropy across layers, indicating less uncertainty in internal representations.
- Accuracy: Only 36.67%, showing that entropy reduction did not align with the classification task.
- Insight: Reducing entropy alone does not ensure the model learns features relevant to classifying Iris samples.

2. SKA Model with Backpropagation:
- Entropy Reduction: Achieved alongside high accuracy (100%).
- Accuracy: Supervised updates ensured that entropy reduction translated into meaningful class distinctions.
- Insight: Backpropagation aligns entropy reduction with the classification goal, making it effective.

3. Traditional Neural Network (SimpleNN):
- Entropy Reduction: Implicitly achieved through cross-entropy loss minimization.
- Accuracy: 100%, with entropy reduction directly tied to classification performance.
- Insight: Supervised learning inherently couples entropy reduction with task-specific accuracy.

Key Takeaway: Entropy reduction correlates with accuracy only when guided by supervision. In the original SKA, entropy decreased without improving accuracy, while the hybrid SKA and SimpleNN leveraged supervision to make entropy reduction meaningful for classification.

## Advantages and Limitations of SKA for the Iris Dataset

Advantages:

* Novel Approach: SKA’s forward-only, entropy-driven learning is innovative and potentially more biologically plausible than backpropagation.
* Hybrid Potential: When paired with backpropagation, SKA achieves high accuracy, suggesting flexibility for hybrid learning systems.
* Unsupervised Potential: The entropy-driven mechanism could be valuable in unsupervised or semi-supervised settings, though this wasn’t fully tested here.

Limitations:

* Inefficient for Small Datasets: For a simple, structured dataset like Iris, traditional backpropagation outperforms SKA in both accuracy and efficiency.
* Task Misalignment: Without supervision, SKA’s entropy reduction doesn’t naturally align with classification, leading to low accuracy (36.67%).
* Convergence Challenges: The original SKA requires many steps without guaranteed convergence, making it less practical for this task.

Key Takeaway: SKA’s strengths lie in its innovative learning paradigm, but it’s less suited for small, well-labeled datasets like Iris, where traditional supervised methods excel. Its potential may be better realized in scenarios with limited labels or continuous learning requirements.

## Conclusion

The experiments show that:

* The original SKA model achieved only 36.67% accuracy after 1000 steps, underperforming due to its reliance on unsupervised entropy reduction.
* The SKA model with backpropagation reached 100% accuracy with fewer steps, matching the traditional neural network (SimpleNN), which also achieved 100% accuracy efficiently.
* For the Iris dataset, traditional backpropagation remains the most effective and efficient approach, while SKA’s entropy-driven framework may offer advantages in more complex, less supervised scenarios.
* Further exploration of SKA could focus on its applicability to unsupervised learning, larger datasets, or tasks requiring adaptability over time.
