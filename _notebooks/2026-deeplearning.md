---
layout: post
title: "Introduction to Deep Learning for Fluids"
topic: "Deep Learning"
tldr: "Neural Networks architectures and frameworks for data-driven modeling."
---

# Deep Learning for Fluid Dynamics

This document was generated from a Jupyter Notebook using `jupyter nbconvert --to markdown`.

Below is an interactive Python example of PyTorch initialization. You can [Download the full .ipynb here](https://raw.githubusercontent.com/...)

```python
import torch
import torch.nn as nn
import numpy as np
import matplotlib.pyplot as plt

# Check for GPU
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
print(f"Using device: {device}")
```

**Output:**
```
Using device: cuda
```

### Simple MLP Definition

```python
class FluidMLP(nn.Module):
    def __init__(self, input_size, hidden_size, output_size):
        super(FluidMLP, self).__init__()
        self.network = nn.Sequential(
            nn.Linear(input_size, hidden_size),
            nn.ReLU(),
            nn.Linear(hidden_size, hidden_size),
            nn.ReLU(),
            nn.Linear(hidden_size, output_size)
        )

    def forward(self, x):
        return self.network(x)

model = FluidMLP(input_size=10, hidden_size=64, output_size=2).to(device)
print(model)
```

**Output:**
```
FluidMLP(
  (network): Sequential(
    (0): Linear(in_features=10, out_features=64, bias=True)
    (1): ReLU()
    (2): Linear(in_features=64, out_features=64, bias=True)
    (3): ReLU()
    (4): Linear(in_features=64, out_features=2, bias=True)
  )
)
```

To contribute a new notebook, simply export your `.ipynb` to Markdown format:
`jupyter nbconvert --to markdown your_notebook.ipynb`

Then drop the resulting `.md` file into the `_notebooks` folder, add the YAML header (title, topic, tldr) at the top, and it will automatically appear in our gallery!
