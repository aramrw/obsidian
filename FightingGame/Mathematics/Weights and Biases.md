#machine-learning

# Weights and Biases

These are the learnable parameters of a neural network, found inside every [[Artificial Neuron]] (or `Detector`) and [[Linear Layer]].

### Weights
Weights determine the strength or importance of an incoming signal. In the codebase, they are conceptualized as "volume knobs". 
- A **high positive weight** means the input is very important for making the neuron "fire".
- A **weight near zero** means the input is mostly ignored.
- A **negative weight** means the input actively discourages the neuron from firing.

### Bias
A Bias is a baseline value added to the score before the final output is determined. It allows the neuron to shift its activation threshold independently of the inputs. For example, if a neuron should only fire if the total input is exceptionally strong, it might have a large negative bias to keep its baseline low. 

When an AI "learns" or "trains", all it is doing is slightly tweaking these Weights and Biases over thousands of iterations until it consistently outputs the right answer.