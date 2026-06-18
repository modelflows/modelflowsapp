---
layout: post
title: "Template: Your Notebook Title Here"
published: false
topic: "Topic Name (e.g. Deep Learning, Data Imputation)"
tldr: "A short, 1-2 sentence description of what your notebook does so people know what to expect."
---

# Template Notebook

This file serves as a placeholder and example for students. To add your own notebook:

1. Write your code in a `.ipynb` Jupyter Notebook.
2. Run `jupyter nbconvert --to markdown your_notebook.ipynb`. 
3. Move the generated `.md` file into the `modelflowsapp/_notebooks/` directory.
4. Add the YAML header block at the exact top of the file (like the title, topic, and tldr block you see when you open this file's source code).

```python
# Your exported python blocks will automatically look like this!
print("Hello ModelFLOWs Notebooks!")
```
