## Immediate Challenges

- EEG is continuous data
- Lots of noise
- Different [[Neurodegenerative Illness]] show different abnormalities in different frequency bands
	- [[Epilepsy]]: 0.5 - 49Hz
	- [[Brain-Computer Interface (BCI)]]: Up to 150Hz
	- Sleep Studies: Alpha brainwaves (8 - 13Hz) or sleep spindle waves (12.5 - 15.5Hz)
- Sampling rates of [[Electroencephalography (EEG)]] devices aren't consistent

## Relevant Papers

### [Neuro-GPT: Towards a foundation model for EEG](https://arxiv.org/abs/2311.03764)

- Used a dataset of 19K EEG from Temple EEG corpus
- Extracted 2s windows
- Used 22 channels to form 10-20 system
- Used average reference (Subtracted average across all channels from each channel)
- Powerline noise removal (60Hz - US)
- Bandpass-filtered (0.5 - 100Hz)
- Resample (250Hz)
- Z-transform along time-dimension to discretise the signal

#### Takeaways 
- Use codewords to quantise the [[Embeddings]] space
	- I.e. map each of the features to a discrete set of values {$1..n$}, using a softmax function to compute the probabilities for these values and picking the value with the highest probability as the value for $k^{th}$ feature 

### [EEGFormer: Towards Transferable and Interpretable Large-Scale EEG Foundation Model](https://arxiv.org/abs/2401.10278)

- [[Transformer]] as base architecture
- Used 12s windows
- Converted signals from frequency domain using FFT
- Used vector quantizer to quantise [[Embeddings]] space
- Reconstructed FFT

### [TOWARDS NEURAL FOUNDATION MODELS FOR VISION: ALIGNING EEG, MEG AND FMRI REPRESENTATIONS TO PERFORM DECODING, ENCODING AND MODALITY CONVERSION](https://arxiv.org/abs/2411.09723)

- Objective was: "Given EEG, [[Functional Magnetic Resonance Imaging (fMRI)]], [[Magnetoencephalography (MEG)]] signals, predict what the person is seeing"
- Interesting for the architecture and information flow

### [LARGE BRAIN MODEL FOR LEARNING GENERIC REPRESENTATIONS WITH TREMENDOUS EEG DATA IN BCI](https://arxiv.org/abs/2405.18765)

- Came up with the LaBram architecture

![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUd8cbFLBXgtJludxZI2GNdsUpNGajLYvKEb29VtFc0PDXeo5a8FFB3gy4loAFSy3CQeX06YByogrf6D4vbNpHqjvdWE4_nbe9_IWXHvmzjCarznPtfsN99jDulHWNBZUgEMTqgjbJnnk-qvWCqSHCLH0OiCSps=s2048?key=yGYlFqcOkUvbKQCmygk7Iw)

- Used DFT to convert signal into time frequency domain
- Quantised embeddings using a neural codebook

![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUeXeJ6pEAekKpxkLWYGglpaShdIzX7FJ93qaJUaTnW8pH9JZCfiDiKsfJFhlqqKrLi7wGetPvJIpqf7qbTXMoAMYhie_chphqHVNrLnBoWH869ZL6V4Dh5aSFhFVQeNi1mXN0P9-RMY6hLb_tyQn3B2Nwqgi0s=s2048?key=yGYlFqcOkUvbKQCmygk7Iw)

## Overall Takeaways

- Reconstruction of embedding space and frequency domain is common across the studies
- Contrastive learning is common across the studies
- Quantising the embedding space is common across the studies
- Converting EEG signals to frequency domain is common across the studies