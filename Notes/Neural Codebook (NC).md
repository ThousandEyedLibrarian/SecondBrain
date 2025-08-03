A learned dictionary that maps continuous data to discrete representations.

*Look, put simply, this is a fucking series of bins, which are just 1-dimensional [[Vectors]] of numerical values.*

Given a set of bins 1-n where each bin is as discrete value representing an EEG voltage at a timestep window.

Collapses model parameter input down massively from a continuous space to a discrete space.

Each value in the codebook is called a "code".

See: [[wav2vec 2.0 - a framework for self-supervised learning of speech representations]]

### How It Works

- Model learns a finite set of "codewords" (vector representations)
- Continuous input gets mapped to nearest codeword
- Replaces infinite variations with manageable discrete set

### Example: Image Compression

- Original image has millions of possible pixel values
- Codebook learns 256 common colour patterns
- Each image patch gets assigned to closest pattern
- Reconstructed using discrete codes instead of raw pixels

### Benefits

- Reduces data complexity and noise
- Creates consistent representations across samples
- Enables efficient processing and comparison
- Discovers meaningful patterns in the data

The codebook vectors are learned during training - the [[Neural Networks (NN)]] model automatically discovers which discrete representations best capture the important features of the input data.