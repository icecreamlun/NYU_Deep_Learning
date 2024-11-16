# Team 45 ACL Submission: Enhanced Accuracy in Mathematical Problem Validation
## An Application of LoRA and Advanced Prompt Engineering

### Authors
- **Zhuolun Li**
  - Email: [zl5583@nyu.edu](mailto:zl5583@nyu.edu)
- **Haolin Yang**
  - Email: [hy2898@nyu.edu](mailto:hy2898@nyu.edu)

## Abstract
This study examines the application of LoRA (Learning rate Annealing and Representation Adjustment) and advanced prompt engineering techniques to improve the accuracy of a language model in validating mathematical problems. We systematically explore various prompt formats and their effect on model performance, detailing both successful strategies and limitations.

## Introduction
Automated validation of mathematical problems presents a complex challenge that requires nuanced understanding from language models. Traditional language models often fall short due to their inability to interpret the specific logical structures and answer correctness within mathematical contexts. Our research focuses on enhancing a pre-trained model's capabilities through the integration of LoRA and tailored prompt engineering, aiming to elevate performance in educational applications.

## Dataset
We employed the "ad6398/nyu-dl-teach-maths-comp" dataset, which comprises a diverse array of mathematical problems tailored for educational purposes. Each entry includes a problem statement, a student's solution, and a boolean correctness label. Our analysis began with a subset of 30,000 entries, carefully selected to ensure diversity in problem type and complexity.

## Model Description
The foundation of our experiments is the "unsloth/Meta-Llama-3.1-8B" model. We enhanced this model using LoRA, which allows for fine-tuning of the model's deep network layers without the extensive computational costs typically associated with training large language models. This technique is particularly effective in adapting pre-trained models to specific tasks such as mathematical validation.

## Experimentation Description and Hyperparameter Settings
Our experimentation involved the iterative development and refinement of various prompt templates designed to guide the model more effectively. Key hyperparameters included:
- **Batch size:** 8, leveraging gradient accumulation to simulate larger batches.
- **Learning rate:** Initiated at 2e-4 with adjustments following a cosine annealing schedule.
- **Epochs:** Set to 3 to balance between overfitting and under-training.
Each training session was interspersed with evaluations every 50 steps to gauge the model's performance dynamically.

## Results
The data highlights how each successive refinement in the prompt structure contributed to incremental accuracy gains, culminating in a significant improvement in the model's ability to correctly validate mathematical solutions.

### Prompt and Training Enhancements
The development of our prompt structure was a pivotal aspect of our model improvement strategy. Initially, in version 1.0, the model achieved a baseline accuracy of 0.48 using basic prompts. In subsequent versions, we incorporated the Solution column into the prompts, which was previously overlooked during training, raising the accuracy to 0.62.

### Scheduled Fine-Tuning (SFT) Improvements
Following the optimization of prompt structures, significant adjustments were made to our training regimen, referred to as Scheduled Fine-Tuning (SFT). These strategic enhancements were designed to optimize training dynamics and improve model performance effectively.

## Appendix: Additional Experiment Details
For further information, please consult the following resources:
- **Model and parameters:** [Google Drive Link](https://drive.google.com/drive/folders/1NBHV4-CpQfSvBMtPstniya3Dsu2YO183?dmr=1&ec=wgc-drive-globalnav-goto)
- **Code repository:** [GitHub Repository](https://github.com/icecreamlun/NYU_Deep_Learning/tree/main)

