## Information

- Paper Title: Predicting Antiseizure Medication Outcomes in Early Diagnosed Epilepsy: A Multimodal Framework Using EEG, MRI, and Clinical Data
- Author(s): Duong Nhu, Jiahe Liu, Richard Shek-kwan Chang, Daniel Thom, Zhibin Chen, Mohamad Nazem-Zadeh, Alison Anderson, Sarah Barnard, Jacqueline French, Patrick Kwan, and Zongyuan Ge
- Year: 2025
- Journal: medRxiv (preprint)
- DOI: https://doi.org/10.1101/2025.03.12.25323644

## Abstract

The paper presents a multimodal deep learning framework for predicting antiseizure medication (ASM) outcomes in patients with newly diagnosed epilepsy. The proposed approach integrates electroencephalography (EEG), magnetic resonance imaging (MRI), clinical factors, and molecular drug features to enhance prediction accuracy. 

The framework includes EEG Q-Net, a pre-trained quantisation model that captures fine-grained temporal EEG patterns, and MRI embeddings from BiomedCLIP. For ASMs, the researchers employed pre-trained models to generate embeddings for SMILES (Simplified Molecular Input Line Entry System) notations, capturing chemical similarities and interactions. 

The multimodal fusion model achieved an AUC of 0.75, demonstrating superior performance compared to the best unimodal model (0.71), highlighting the benefits of multimodal integration for personalised epilepsy management.

## Key Points

- Proposed multimodal framework integrates EEG, MRI, clinical data, and molecular drug features
- Developed EEG Q-Net for capturing temporal patterns in EEG signals
- Used BiomedCLIP for extracting features from MRI scans
- Employed pre-trained models for generating SMILES embeddings of ASMs
- Multimodal approach outperformed individual modalities for ASM outcome prediction
- System designed to be easily translatable to clinical practice using routinely collected data

## Personal Notes

### Clinical Challenge

- Epilepsy affects 50 million people worldwide with recurrent seizures
- 1/3 of patients don't respond to available medications (25+ different drugs)
- Current process: Trial-and-error approach leading to years of ineffective treatment
- Consequences: Reduced quality of life, hospitalizations, increased mortality, economic burden

### AI Opportunity

- Standard diagnosis includes EEG and MRI scans - readily available data
- Previous AI attempts used only clinical factors with poor performance (~low AUC)
- Genomic approaches showed promise but are expensive and not widely covered by insurance

### Technical Architecture

### Data Modalities (4 types)

#### 1. EEG (Electroencephalogram)

- Input: 20-minute brain electrical recordings from 19 electrodes
- Preprocessing:
    - 10-second windows (fixed-length segment extracted from a continuous signal for analysis), downsampled to 256 Hz
    - Filtered 0.5-70 Hz, artifact removal via FASTER algorithm
    - Average referencing, log-normalization
- Challenge: Infinite variability across patients/devices limits model generalizability

#### 2. MRI (Magnetic Resonance Imaging)

- Input: T1-weighted brain structural scans
- Preprocessing:
    - Standardized to RAS+ orientation
    - Middle slice extraction from axial, coronal, sagittal views
    - Min-max normalization (0-255 intensity)
    - Brightness/contrast/sharpness enhancements

#### 3. Clinical Factors

- Variables: 16 key factors including age (4 categories), sex, alcohol abuse, psychological disorders
- Encoding: Integer categories starting from 1, missing data as 0
- Basis: Literature-validated factors linked to medication outcomes

#### 4. Drug Molecular Structure

- SMILES strings: Chemical structure notation (e.g., 'CC(=O)N1CCCC1C2CCOC2' for levetiracetam)
- Purpose: Capture drug similarities beyond simple categorical encoding

### Novel Technical Contributions

### EEG Q-Net: Pre-trained Quantization Model

#### Architecture Inspiration

- Based on wav2vec 2.0 (speech recognition) adapted for EEG signals
- Addresses continuous signal variability through discretization

#### Core Components

1. Quantization: Maps continuous EEG to discrete codewords using product quantization
    - 10 [[Neural Codebook (NC)]]s with 18 codewords each
    - Gumbel softmax for probabilistic codeword selection
    - Temperature decay: $2.0 \rightarrow 0.5$
    
    Technical Implementation:
    - Product Quantization: Splits high-dimensional vectors into subvectors, quantizes each separately
    - Gumbel Softmax: Differentiable sampling method allowing gradient flow through discrete selections
    - Temperature Annealing: High temp = random selection, low temp = deterministic selection

2. Masking Strategy:
    - Randomly sample $N=5$ timesteps
    - Mask $M=10$ consecutive steps
    - Forces model to learn contextual relationships
    
    Technical Implementation:
    - Contiguous Masking: Removes temporal chunks rather than random points
    - [[Self-Supervised Learning]]: Model predicts masked content from surrounding context
    - Temporal Dependencies: Learns long-range EEG patterns crucial for epilepsy detection

3. Context Learner:
    - S4D (Structured State Space) model fills masked representations
    - 16 S4D blocks, state size 512, dimension 128
    
    Technical Implementation:
    - State Space Models: Efficiently model long sequences via linear recurrent structure
    - S4D Variant: Diagonal state matrices for computational efficiency
    - Bilinear Transform: Maps continuous-time dynamics to discrete-time processing

4. [[Loss Function]]:
    - Contrastive loss: $L_m$ (temperature=0.1, cosine similarity)
    - Diversity regularization: $L_d$ prevents codeword collapse
    - Combined: $L = L_m + \alpha L_d$ where $\alpha=0.2$
    
    Technical Implementation:
    - Contrastive Learning: Pulls positive pairs together, pushes negative pairs apart
    - Temperature Scaling: Controls sharpness of similarity distributions
    - Diversity Loss: $L_d = \frac{1}{E}\sum_{e} p_e \log p_e$ ensures balanced codebook usage

#### Training Details

- [[Adaptive Moment Estimation (ADAM)]]W optimiser, learning rate $1 \times 10^{-4}$, weight decay $0.1$
- Cosine annealing with warm restarts every 20 epochs
- 200 negative samples per minibatch
- Minimum 100 epochs, early stopping after 10 epochs without improvement

Technical Implementation:

- AdamW: Adam with decoupled weight decay for better generalisation
- Cosine Annealing: Cyclical learning rate schedule preventing local minima
- Negative Sampling: Random timesteps from other EEGs in batch as contrastive examples

### Drug Embedding Methods

#### SMILES Representation

- MoLER: Graph-based model accounting for molecular scaffolds and chemical bonds
- MTE (Molecular Transformer Embeddings): End-to-end transformer encoder
- Output: 512-dimensional vectors capturing chemical relationships
- Advantage: Generalises to unseen medications based on structural similarity

Technical Implementation:

- Graph Neural Networks: MoLER processes molecular graphs with attention mechanisms
- [[Transformer]] Architecture: MTE treats SMILES as sequences, learns character-level patterns
- Chemical Similarity: Embedding distance correlates with pharmacological similarity

### MRI Feature Extraction

- BiomedCLIP: Vision-language foundation model pre-trained on large MRI corpus
- Comparison: Axial-only vs multi-view (axial + coronal + sagittal)
- Output: 512-dimensional feature vectors

Technical Implementation:

- Vision Transformer: CLIP uses ViT backbone for image encoding
- Multi-View Fusion: Concatenates features from three anatomical planes
- Transfer Learning: Pre-trained weights fine-tuned for epilepsy-specific features

### Model Architecture & Training

### Fusion Strategy

1. Unimodal Training: Each modality trained separately with SMILES embeddings
2. Best Model Selection: Highest AUC and AUPRC scores per modality
3. Multimodal Fusion: Concatenate best embeddings → MLP fusion layer

### Network Design

- MLPs: 3 blocks each (Linear → ReLU ([[Activation Function]]) → Dropout → LayerNorm)
- EEG Processing: S4D network with 8 layers
- Optimisation: Direct AUC maximisation using PDSCA optimiser
- Class Balance: Equal seizure-free/not seizure-free samples per minibatch (16 total)

Technical Implementation:

- Late Fusion: Combines learned representations rather than raw features
- PDSCA Optimiser: Primal-Dual method specifically designed for AUC optimisation
- Compositional Loss: $\text{AUC} = P(f(x_+) > f(x_-))$ optimised directly

### Training Configuration

- Cosine annealing for outer/inner learning rates
- Learning rates: $0.05$, weight decay: $0.1$
- Inner steps: $2$, minimum 50 epochs
- Early stopping: 10 epochs without validation AUC improvement

Technical Implementation:

- Bi-level Optimisation: Outer loop updates model, inner loop optimises AUC surrogate
- Learning Rate Scheduling: Prevents overshooting in final training phases
- Patience-Based Stopping: Prevents overfitting while ensuring convergence

### Dataset & Evaluation

### Data Sources

- HEP1: International multicentre study (2012-2020), newly diagnosed focal epilepsy
- Alfred Health: Australian hospital dataset (2018-2022)
- Total: 357 patients (85 seizure-free, 272 not seizure-free)
- Medications: 7 first-line ASMs (levetiracetam, carbamazepine, valproate, etc.)

### Outcome Definition

- Success: No seizures for 12 months on initial monotherapy
- Failure: Therapy changes within 12-month period

### Evaluation Metrics

- Primary: AUC (Area Under ROC Curve)
- Secondary: Sensitivity, Specificity, Precision, AUPRC
- Validation: 5-fold cross-validation
- Threshold: Maximised balanced accuracy on training set

Technical Implementation:

- Stratified K-Fold: Maintains class distribution across folds
- ROC-AUC: $\text{AUC} = \int_0^1 \text{TPR}(t) , d\text{FPR}(t)$
- Balanced Accuracy: $\frac{1}{2}(\text{Sensitivity} + \text{Specificity})$

### Results & Performance

### Unimodal Performance

|Modality|Best Configuration|AUC (SD)|Key Findings|
|---|---|---|---|
|Clinical + SMILES|MTE embeddings|$0.71 \pm 0.05$|Baseline performance|
|MRI + SMILES|Multi-view + MTE|$0.69 \pm 0.06$|Multi-view > axial only|
|EEG + SMILES|Latent + MTE|$0.64 \pm 0.02$|Higher precision than others|
|Clinical (one-hot)|Traditional encoding|$0.68 \pm 0.02$|SMILES > one-hot|

### Multimodal Performance

|Configuration|AUC (SD)|Improvement|
|---|---|---|
|All modalities|$0.75 \pm 0.07$|+4 points over best unimodal|
|EEG + Clinical|$0.74 \pm 0.07$|+3 points|
|MRI + Clinical|$0.71 \pm 0.06$|Baseline level|

### Key Performance Insights

- SMILES advantage: Outperformed one-hot encoding by 3 AUC points
- Modality complementarity: Each contributes unique predictive information
- Multi-view MRI: Superior to single-plane imaging for epilepsy prediction
- EEG precision: Highest precision scores despite lower overall AUC

### Technical Significance & Innovation

### Methodological Advances

1. First multimodal approach combining EEG, MRI, clinical data, and molecular features for ASM prediction
2. Novel EEG quantisation: Addresses fundamental signal variability challenge
3. Chemical-aware drug representation: Enables generalisation to unseen medications
4. Foundation model integration: Leverages pre-trained models for improved feature extraction

Technical Implementation:

- Modality-Specific Encoders: Specialized architectures for each data type
- Cross-Modal Attention: Future work could explore attention mechanisms between modalities
- Domain Adaptation: Transfer learning strategies for new hospitals/populations

### Clinical Translation Potential

- Cost-effective: Uses routine diagnostic data (no expensive genomic testing)
- Practical implementation: Standard hospital workflows
- Personalised medicine: Patient-specific treatment recommendations
- Reduced trial-and-error: Faster identification of effective treatments

### Limitations & Future Work

- 2D MRI limitation: May need 3D models for better structural anomaly detection
- Missing modality handling: Need robust methods when some data unavailable
- Dataset size: Relatively small for [[Deep Learning]] (357 patients)
- Validation scope: Single-center external validation needed

## Methodology

- Dataset combined patients from Human Epilepsy Project (HEP1) and Alfred Health Hospital in Australia
- Developed EEG Q-Net framework with quantisation representation, masking, and context learning using Structured State Space models (S4)
- Extracted SMILES notations for ASMs from Drugbank
- Tested two SMILES embedding approaches: MoLER (graph-based) and Molecular Transformer Embeddings (MTE)
- Employed BiomedCLIP, a vision-language foundation model, to extract features from MRI scans
- Compared single-view (axial) vs multi-view (axial, coronal, sagittal) MRI approaches
- Used multilayer perceptron (MLP) fusion architecture to combine modality-specific embeddings
- Optimised AUC directly using compositional AUC loss with Primal-Dual Stochastic Compositional Adaptive optimiser

## Results

- Multimodal approach achieved best performance with AUC of 0.75 (SD: 0.07)
- Clinical factors with SMILES embeddings achieved AUC of 0.71 for both MoLER and MTE
- SMILES embeddings outperformed ASM one-hot encoding (AUC: 0.68)
- EEG embeddings achieved AUC of 0.64
- MRI multi-view embeddings achieved AUC of 0.69
- Combination of EEG embeddings with clinical factors improved AUC to 0.74
- While EEG and MRI models had lower AUCs than clinical-factor models, the best EEG models had higher precision

## Conclusions

- Integration of multiple data modalities enhances ASM outcome prediction compared to unimodal approaches
- SMILES embeddings provide a more effective representation of drugs than one-hot encoding
- Multi-view MRI approach captures more comprehensive structural information than single-view
- The framework can be adapted for ASM selection by using prediction probabilities to guide treatment decisions
- Multimodal approach lays foundation for personalised epilepsy management using routinely collected clinical data

## Quotations

> "Our findings underscore the benefits of multimodal integration for personalised epilepsy management, as our fusion model achieved an AUC of 0.75, an improvement over the best unimodal model (0.71)."

> "Uncontrolled seizures can cause substantial health, psychosocial, and economic impacts to patients, including increased hospitalisation, comorbidities, premature mortality, and decreased quality of life."

## References to Follow Up

- BiomedCLIP [25] - A vision-language foundation model trained on medical images
- MoLER [14] - Graph-based model for molecular embedding
- Molecular Transformer Embeddings (MTE) [15] - End-to-end transformer encoder for SMILES embedding
- Structured State Space models (S4) [9] - Method for quantising signals through bilinear transformation

## Literature Review Sections

- Current ASM outcome prediction approaches
    - Limitations of clinical factor-based models
    - Integration of genetic information
    - Potential of neuroimaging biomarkers
- Deep learning approaches for EEG and MRI analysis
    - Quantisation methods for EEG signal processing
    - Foundation models for medical image analysis
    - Multimodal fusion strategies

## Research Questions

- How can multimodal deep learning improve personalised epilepsy treatment?
- What is the relative contribution of each modality to prediction accuracy?
- Can pre-trained embeddings for molecular drug structures enhance generalisability?
- How effective are foundation models in extracting features from medical imaging data?

## Gaps in the Literature

- Limited use of raw EEG and MRI data in ASM outcome prediction
- One-hot encoding inadequately captures drug relationships
- Need for cost-effective alternatives to genome sequencing
- Lack of comprehensive multimodal approaches in epilepsy management

## Synthesis

The integration of multimodal data through specialised deep learning architectures represents a significant advancement in epilepsy treatment personalisation. By leveraging routinely collected clinical, neurophysiological, and neuroimaging data, the proposed framework offers a practical approach to ASM selection that could potentially reduce the trial-and-error period often experienced by patients. The use of pre-trained models for feature extraction from complex data types demonstrates the value of transfer learning in medical applications with limited training data.

## Ideas for Future Research

- Specialised 3D MRI models to better capture structural abnormalities
- Methods for handling missing modalities in clinical practice
- Refined co-embedding techniques to optimise multimodal data fusion
- Prospective clinical validation of the prediction framework
- Extension to multi-drug therapy prediction for refractory epilepsy
- Integration of longitudinal data to capture disease progression


See also:
- [[Brain-Computer Interface (BCI)]]
- [[Computational Neuroscience]]
- [[Machine Learning]]