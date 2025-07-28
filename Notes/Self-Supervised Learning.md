Trains [[Neural Networks (NN)]] models without labeled data by creating prediction tasks from the data itself.

### How It Works

- Model creates its own training targets from input structure
- Masks/hides parts of data, tries to predict missing pieces
- Uses signal patterns to learn meaningful representations

### Example: [[Electroencephalography (EEG)]] Masking

- Take 20-minute EEG recording
- Randomly mask 10 consecutive timesteps (hide brain activity)
- Model learns to predict masked activity from surrounding context
- Forces learning of temporal brain signal patterns

### Benefits

- No manual labelling required (expensive for medical data)
- Learns general EEG patterns before specific [[Epilepsy]] task
- Captures temporal dependencies in brain signals
- Pre-trained model transfers to epilepsy prediction

The masking forces the model to understand how [[Brain]] signals evolve over time.