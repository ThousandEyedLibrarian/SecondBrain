A learned dictionary that maps continuous data to discrete representations.

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