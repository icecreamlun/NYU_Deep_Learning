\documentclass[11pt]{article}
\usepackage[review]{ACL2023}
\usepackage{times}
\usepackage{latexsym}
\usepackage[T1]{fontenc}
\usepackage[utf8]{inputenc}
\usepackage{microtype}
\usepackage{graphicx} % For including graphics
\usepackage{booktabs} % For formal tables
\usepackage{tabularx} % Add this line in the preamble
\usepackage{hyperref} % Add this line if it's not already in your preamble


\title{Team 45 ACL Submission: Enhanced Accuracy in Mathematical Problem Validation: An Application of LoRA and Advanced Prompt Engineering}

\author{
  Zhuolun Li \\
  Affiliation / Address line 1 \\
  Affiliation / Address line 2 \\
  \texttt{zl5583@nyu.edu} \\\And
  Haolin Yang \\
  Different Affiliation / Address line 1 \\
  Address line 2 \\
  \texttt{hy2898@nyu.edu} \\
}

\begin{document}
\maketitle

\begin{abstract}
  This study examines the application of LoRA (Learning rate Annealing and Representation Adjustment) and advanced prompt engineering techniques to improve the accuracy of a language model in validating mathematical problems. We systematically explore various prompt formats and their effect on model performance, detailing both successful strategies and limitations.
\end{abstract}

\section{Introduction}

Automated validation of mathematical problems presents a complex challenge that requires nuanced understanding from language models. Traditional language models often fall short due to their inability to interpret the specific logical structures and answer correctness within mathematical contexts. Our research focuses on enhancing a pre-trained model's capabilities through the integration of LoRA and tailored prompt engineering, aiming to elevate performance in educational applications.

\section{Dataset}

We employed the "ad6398/nyu-dl-teach-maths-comp" dataset, which comprises a diverse array of mathematical problems tailored for educational purposes. Each entry includes a problem statement, a student's solution, and a boolean correctness label. Our analysis began with a subset of 30,000 entries, carefully selected to ensure diversity in problem type and complexity.

\section{Model Description}

The foundation of our experiments is the "unsloth/Meta-Llama-3.1-8B" model. We enhanced this model using LoRA, which allows for fine-tuning of the model's deep network layers without the extensive computational costs typically associated with training large language models. This technique is particularly effective in adapting pre-trained models to specific tasks such as mathematical validation.

\section{Experimentation Description and Hyperparameter Settings}

Our experimentation involved the iterative development and refinement of various prompt templates designed to guide the model more effectively. The following hyperparameters were pivotal in our experiments:
- \textbf{Batch size:} 8, leveraging gradient accumulation to simulate larger batches.
- \textbf{Learning rate:} Initiated at 2e-4 with adjustments following a cosine annealing schedule.
- \textbf{Epochs:} Set to 3 to balance between overfitting and under-training.

Each training session was interspersed with evaluations every 50 steps to gauge the model's performance dynamically.

\section{Results}

{\small % This will apply the small font size to everything within the braces
\begin{table}[h]
\centering
\begin{tabularx}{0.5\textwidth}{Xcc} % Adjusting table width to half the text width
\toprule
\textbf{Version} & \textbf{Initial} & \textbf{Final} \\
\midrule
Basic Prompt               & 0.05 & 0.48 \\
Solution Inclusion         & 0.48 & 0.62 \\
Rule-based Enh.            & 0.62 & 0.71 \\
Problem Type Seg.          & 0.71 & 0.72 \\
Final Refined Prompts      & 0.72 & 0.835\\
\bottomrule
\end{tabularx}
\caption{Accuracy improvements with prompt versions.}
\label{tab:prompt_versions}
\end{table}
} % End of \small scope


The data in Table \ref{tab:prompt_versions} highlights how each successive refinement in the prompt structure contributed to incremental accuracy gains, culminating in a significant improvement in the model's ability to correctly validate mathematical solutions.

\subsection{Prompt and Training Enhancements}

The development of our prompt structure was a pivotal aspect of our model improvement strategy. Initially, in version 1.0, the model achieved a baseline accuracy of 0.48 using basic prompts. In subsequent versions, we incorporated the Solution column into the prompts (version 1.1), which was previously overlooked during training, raising the accuracy to 0.62.

Further enhancements included the integration of detailed rule-based guidance for solving problems (version 1.2), which improved the accuracy to 0.71. Recognizing the importance of tailored prompts, we segmented problems based on the type of solution in version 1.3, which slightly improved accuracy to 0.72, and based on the type of problem in version 1.4, which refined the approach to achieve an accuracy of 0.73. Version 1.5 attempted to merge these strategies, but it did not surpass the performance of version 1.4, stabilizing at an accuracy of 0.72.

\subsection{Evolution of Prompt Structures}

As part of our iterative refinement process, the structure of the prompts used to guide the model's understanding and response accuracy was significantly enhanced. Below, we outline the progression of these prompt structures, demonstrating the strategic enhancements made at each stage:

\subsubsection{Version 1.0: Basic Prompt}
Initially, the prompt was straightforward, focusing solely on whether the student's answer was correct, without providing any context or guidance on how to evaluate the answer:
\begin{quote}
"You are a great mathematician and you are tasked with finding if an answer to a given maths question is correct or not. Your response should be 'True' if correct, otherwise 'False'. Below is the Question and Answer.

### Question:

### Answer:

### Explanation

### Output:"
\end{quote}

\subsubsection{Version 1.1: Solution Inclusion}
Responding to the need for a more context-aware model, the prompt was enhanced by including a segment to evaluate the solution, urging the model to consider the content of the solution during validation:
\begin{quote}
"You are a great mathematician and you are tasked with finding if an answer to a given maths question is correct or not. Your response should be 'True' if correct, otherwise 'False'. Below is the Question, Answer, and Explanation. To solve this question accurately, consider the provided solution.

### Question:

### Answer:

### Solution:

### Output:"
\end{quote}

\subsubsection{Version 1.2 to 1.4: Enhanced Guidance and Specialization}
Further enhancements introduced detailed validation processes and formatting considerations, especially for LaTeX expressions, which are commonly used in mathematical notation. These versions began to differentiate the types of mathematical problems, applying specific templates tailored to the characteristics of problems such as arithmetic, algebra, and geometry:
\begin{quote}
"You are a great mathematician and you are tasked with finding if an answer to a given maths question is correct or not. Your response should be 'True' if correct, otherwise 'False'. Below is the Question, Answer, and Explanation. To solve this question accurately, use code if necessary.

### Validation Process:
1. Focus on the QUESTION and STUDENT ANSWER:
   - Understand what the question is asking for.
   - Evaluate if the student's answer makes mathematical sense.
   - Check if the answer format matches the question requirements.

2. Mathematical Correctness:
   - Verify if the answer satisfies the question conditions.
   - Check if the mathematical expression is valid.
   - Ensure the answer is in the correct domain.

3. Format Considerations:
   - Ensure LaTeX expressions are properly formatted.
   - Verify the correctness of any dimensional constraints.

### Question:

### Answer:

### Explanation:

### Output:"
\end{quote}

These prompt modifications not only provided the model with clearer guidance on how to assess responses but also aligned the training process more closely with the nuanced requirements of mathematical problem validation. The evolution of these prompts reflects our approach to progressively refining the interaction between the user's input and the model's evaluation capabilities.

\subsection{Scheduled Fine-Tuning (SFT) Improvements}

Following the optimization of prompt structures, significant adjustments were made to our training regimen, referred to as Scheduled Fine-Tuning (SFT). These strategic enhancements were designed to optimize training dynamics and improve model performance effectively:

\begin{itemize}
    \item \textbf{Batch Size and Gradient Accumulation:} We increased the per-device train batch size to 8, along with matching the gradient accumulation steps to 8. This change allowed us to simulate a larger effective batch size, enhancing the stability of the model's updates and speeding up the training process by increasing data throughput per training instance.
    
    \item \textbf{Training Duration and Warm-Up Phase:} The training was structured to complete three full epochs. We transitioned from a fixed number of warm-up steps to a warm-up phase that constituted 10\% of the total training steps. This proportionate approach allows for a more flexible and scalable adaptation to varying dataset sizes and complexities, ensuring that the learning rate is optimally increased from a lower initial value to the set learning rate in a way that matches the learning dynamics of the model.
    
    \item \textbf{Learning Rate Scheduler:} We shifted from a linear to a cosine learning rate scheduler. Unlike the linear scheduler, which reduces the learning rate uniformly over time, the cosine scheduler decreases the learning rate following a cosine curve, facilitating more nuanced adjustments. This method often leads to better convergence in later stages of training by allowing fine-grained control over the learning rate as it approaches lower values.
    
    \item \textbf{Periodic Evaluations:} To continuously monitor and adjust the training's efficacy, we introduced periodic evaluations every 50 steps, utilizing approximately 10\% of the training data as an evaluation set. This frequent assessment helps in identifying the best model configurations during the training process and making necessary adjustments based on real-time performance metrics.
\end{itemize}

These SFT enhancements significantly boosted the model's performance, elevating the accuracy from 0.72 in version 1.3 of our prompt structure to a range between 0.82 and 0.83 in version 1.4. The introduction of a nuanced warm-up period and a cosine learning rate scheduler, in particular, were pivotal in achieving these gains, as they tailored the learning process more closely to the model's needs and the specific challenges posed by the dataset.


\subsection{Final Adjustments and Outcomes}

Our final tuning involved scaling the training data. Initially, we utilized a dataset of 10,000 entries, achieving an accuracy of 0.83. By expanding the training set to 30,000 entries (with a corresponding evaluation set increase), we marginally improved our model's accuracy to 0.835, effectively demonstrating the benefits of larger datasets in training robustness.

These systematic enhancements to both the prompts and the training processes underscore the efficacy of iterative refinement and targeted adjustments in achieving superior model performance.

\section{Conclusion}

The combination of LoRA with strategic prompt engineering yielded a significant improvement in model accuracy for mathematical problem validation tasks. Future work will explore the integration of additional natural language processing techniques and further prompt refinement to address the remaining challenges and limitations encountered during this study.

\section*{Acknowledgements}

We thank NYU Tandon for supporting this research.

\bibliography{references}
\bibliographystyle{acl_natbib}

\appendix
\section{Appendix: Additional Experiment Details}

Details on the specific configurations of the LoRA parameters and additional experiments that were conducted can be found here. For further information, please consult the following resources:

\begin{itemize}
    \item Model and parameters: \url{https://drive.google.com/drive/folders/1NBHV4-CpQfSvBMtPstniya3Dsu2YO183?dmr=1&ec=wgc-drive-globalnav-goto}
    \item Code repository: \url{https://github.com/icecreamlun/NYU_Deep_Learning/tree/main}
\end{itemize}

\end{document}
