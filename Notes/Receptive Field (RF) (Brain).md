Think of receptive fields as the specific patch of sensory space that a [[Neuron]] calls its turf - basically, it's the spatial region where stimuli can trigger that neuron to fire up (or shut down). 

In vision, for instance, each neuron in your visual system responds to stimuli from a particular area of your visual field which comes from your optical nerve, with some neurons getting excited by light and others by darkness, or some responding to vertical lines while others prefer horizontal ones. 

The beauty of receptive fields is how they hierarchically stack up through the neural pathway - early sensory neurons have tiny receptive fields that detect basic features, while higher-up neurons combine these to respond to increasingly complex patterns. It's like going from pixels to portraits in your [[Brain]]'s processing pipeline.

## Types
- On-centre, off-surround: Cell responds when you turn on input (light for example) in the centre, and responds when you turn off a spot of light in the surrounding region
- Off-centre, on-surround: Vice versa

The On-Center / Off-Surround receptive field can be thought of as a filter. This filter results in more activation due to certain stimuli, and a depression in activation due to other stimuli.

## The Nitty-Gritty Details

Mathematically, we can model receptive fields as spatiotemporal filters with specific response properties:

$RF(x,y,t) = ∑ w_i * I(x,y,t) + b$

where:
- $RF(x,y,t)$ is the receptive field response at position (x,y) and time t
- $w_i$ are synaptic weights
- $I(x,y,t)$ is the input stimulus
- $b$ is the baseline firing rate

Key characteristics include:

- **Center-surround organisation**: Often modelled as difference-of-Gaussians (DoG)
	- $DoG = Ac*exp(-(x²+y²)/2σc²) - As*exp(-(x²+y²)/2σs²)$
- **Spatiotemporal dynamics**: Response properties change with both space AND time
- **Non-linear integration**: Many RFs show non-linear summation of inputs (think divisive normalisation)
- **Adaptation**: RF properties dynamically adjust based on context (gain control)

*The average V1 (AKA striate visual cortex, AKA primary visual cortex) simple cell has a receptive field about 1° of visual angle in size, roughly your thumbnail at arm's length. These buggers then tile your entire visual field like a massive, dynamic signal processing array!* 

## Using a Monkey Example

- Place an electrode next to a [[Brain Cell]] in a monkey visual cortex
- Train the monkey to stare at a fixation spot without moving its eyes
- Stimulate various regions of visual space
- A cell will respond to stimulation in one part of space more than any others
- The region of visual space that drives that particular cell forms its receptive field

Different cells have different RFs, some are tuned into other properties as mentioned above, e.g. shape, colour, direction of motion, etc.

Nearby cells in the cortex have nearby receptive fields, producing [[Retinotopic Maps]], whatever the fuck that means...

Note that each cortex has its own map, touch, audio, etc.