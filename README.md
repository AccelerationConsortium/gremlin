# cartoGraphy foR mixEd MetaL oxIdes syNthesis (GREMLIN)
Kernel learning guided high-throughput synthesis and characterization of mixed metal oxides 

![Figure-workflow](https://github.com/user-attachments/assets/34a452eb-c0c7-43e3-895d-2cb0b792c882)

What if you could go beyond just predicting success from limited high-throughput data and actually understand which regions of your experimental design space are most likely to work, and why?🔬

We explored this on the synthesis of the Fe₂(ZnCo)O₄ mixed metal oxide spinel using a robotic platform, and identified the key conditions for forming a single, stable phase via kernel learning and explainable AI. This was done by defining a global SHAP analysis across a synthetically generated design space to interpret which parameters most positively influence synthesizability. Interestingly, even from the very limited data, our model's explainability aligns well with theory. Global SHAP is particularly useful if you're looking for comprehensive, interpretable insights into the average behavior of a model across a dataset, rather than focusing only on individual instance-level explanation.

## Kernel Learning

we leverage kernel learning and the SHapley Additive exPlanations (SHAP) to interpret the influence of synthesis conditions for the single-phase formation of a ternary spinel system Fe2(ZnCo)O4. Specifically, all samples are synthesized using a Chemspeed automation platform for better reproducibility and precious parameter control across the synthesis space. A kernel classification model is trained with the sparse independent experimental conditions including reagent concentrations, the amount of reagents, the reagent addition rate, and reagent addition
order as features for single-phase synthesis. Kernel methods are performed in two successive steps: First, the training data in
the input space is mapped onto a higher dimensional feature space, where sometimes even unknown features are induced by the kernel. In the second step, a linear method is applied to find a linear relationship in that feature space in a regression or a classification setting. Since everything
is formulated in terms of kernel-evaluations, there is no need for any explicit calculations in the high-dimensional feature space

### Performance and Calibration 

![model_performance_metrics](https://github.com/user-attachments/assets/0e7fb2ce-9bea-4c46-9135-49b8ac418652)

A)
Absolute correlation matrix of the selected experimental features using Pearson’s correlation coefficient.
Other features with correlation >= 0.55 are considered highly correlated, thus, disregarded.
B) Confusion matrix for the binary classification of the solution’s phase. The leave-one-out crossvalidation
(LOOCV) accuracy and AUC are, 0.843 and 0.836, respectively. C) The calibration
curve shows that the model’s predicted probabilities align with observed frequencies of single-phase
outcomes, with some natural zigzagging due to sparse bin populations in LOOCV.)

![model_calibration](https://github.com/user-attachments/assets/05219b84-759f-4e9f-b530-3d401f2a7b49)

Kernel model calibration assessment. The high uncertainty threshold was set at the 66th
percentile (0.47). A) Distribution of kernel model’s disagreements (errors) in the missing region by
uncertainty level and class. B) Probability vs uncertainty of all samples in the missing region. 100%
of the multi-phase errors (FP) occur in the high uncertainty region, while most correct predictions
(TP/TN) cluster in the low uncertainty regions with higher confidence (probabilities further from
0.5), demonstrating appropriate model calibration.

## Golbal SHAP

![F-contour-label](https://github.com/user-attachments/assets/32ce0ca9-9709-4846-8fcb-1dd6acdbed20)

Contour plots of the global SHAP values for different pairs of experimental features,
aggregated over the synthetic space of 43,000 experiment samples. The phase of the binary spinel is
inferred by the kernel classifier, and the global SHAP value offers a comprehensive view of how
each feature combination positively influences single-phase formation in alignment with theoretical
and experimental expectations. Within the K2CO3 concentration range of 0.15–0.3 M, all samples
exhibit at least one secondary phase, creating a missing region (marked with red) with very few
single-phase outcomes (panel C). Despite additional experiments confirming single-phase synthesis
is possible, the overall success rate in this region remains significantly lower than elsewhere,
underscoring the distinct effect of K2CO3 on phase formation.

