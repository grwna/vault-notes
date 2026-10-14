# The Chain Rule:
How to read the notation (partial derivative with respect to something):
$$\frac{\partial x}{\partial y}$$
This means if we nudge $y$ by a certain amount, what is the corresponding change for $x$?. This will be used to measure how changes to the *weights* affect the *cost*.

## Single Neuron Layers
A **connection** between the last *hidden* layer ($L-1$) to the *output* layer ($L$) has these components:
**NOTE:** $L$ is the index of layer, starting from the output layer and moves backward to the input.
- Weight of the connection ($w^L$)
- Raw output from $L-1$ to $L$   ($z^L$), equivalent to ($w^L\times a^{L-1}\times b^L$)
- Activated output from $L-1$ to $L$   ($a^L$)
- Cost ($C$)

**What we want to know:** what effect does changing the weights have to the value of the cost?
**In other words**: the value of:
$$\frac{\partial C}{\partial w^L}$$
All this is for a single item in the gradient vector, and for a single training data. Averaging is required to calculate for all training data. And the step described above only covers tha backpropagation of the output layer to the last hidden layer, while back propagation needs to be done to all layers.

Also, if we want to know the effect of changing the bias towards the cost, we can do so by just substituting $w^L$ with $b^L$.


## Multiple Neuron Layers
Instead of only taking into account the layers, (e.g $a^L$), we also need to take into account the neurons: (e.g. $a^L_{i}$).