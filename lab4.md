import numpy as np
import matplotlib.pyplot as plt

class Neuron:
    def __init__(self, n_inputs, bias=0., weights=None):
        self.b = bias
        if weights is not None:
            self.ws = np.array(weights)
        else:
            self.ws = np.random.rand(n_inputs)

    def _f(self, x):
        return max(x * 0.1, x)

    def __call__(self, xs):
        return self._f(xs @ self.ws + self.b)


n_inputs = 3
n_hidden1 = 4
n_hidden2 = 4
n_outputs = 1

input_layer = [Neuron(n_inputs) for _ in range(n_inputs)]
hidden_layer1 = [Neuron(n_inputs) for _ in range(n_hidden1)]
hidden_layer2 = [Neuron(n_hidden1) for _ in range(n_hidden2)]
output_layer = [Neuron(n_hidden2) for _ in range(n_outputs)]


def visualize_network():
    fig, ax = plt.subplots(figsize=(6, 6))


    layer_sizes = [n_inputs, n_hidden1, n_hidden2, n_outputs]
    max_layer_size = max(layer_sizes)
    v_spacing = 1.0 / (max_layer_size + 1)
    h_spacing = 1.1 / (len(layer_sizes) + 1)


    positions = {}
    for i, layer_size in enumerate(layer_sizes):
        layer_x = (i + 1) * h_spacing
        layer_y = np.linspace(1 - v_spacing, v_spacing, layer_size)
        for j in range(layer_size):
            positions[(i, j)] = (layer_x, layer_y[j])

    positions[(len(layer_sizes) - 1, 0)] = (positions[(len(layer_sizes) - 1, 0)][0],
                                            positions[(len(layer_sizes) - 1, 0)][1] - v_spacing / 0.65)

    colors = ['pink', 'lightblue', 'lightblue', 'lightgreen']

    for (i, j), (x, y) in positions.items():
        layer_index = i
        circle = plt.Circle((x, y), v_spacing / 3.7, color=colors[layer_index], ec='k', zorder=4)
        ax.add_artist(circle)

    for i in range(len(layer_sizes) - 1):
        for a in range(layer_sizes[i]):
            for b in range(layer_sizes[i + 1]):
                x1, y1 = positions[(i, a)]
                x2, y2 = positions[(i + 1, b)]
                line = plt.Line2D([x1, x2], [y1, y2], c='k')
                ax.add_artist(line)

    for j in range(n_inputs):
        x, y = positions[(0, j)]
        plt.text(x - 0.08, y, f'Input {j + 1}', ha='right', va='center', fontsize=8)
    for j in range(n_outputs):
        x, y = positions[(len(layer_sizes) - 1, j)]
        plt.text(x + 0.08, y, f'Output {j + 1}', ha='left', va='center', fontsize=8)

    ax.set_aspect('equal')
    ax.set_xticks([])
    ax.set_yticks([])
    ax.axis('off')
    plt.show()


visualize_network()
