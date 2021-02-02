---
title: Writing LaTex formulas in GitHub pages website
layout: post
category: Coding
---

Among those hosting their website on GitHub pages, many will have a mathematical orientation. However, the markdown language used by GitHub pages does not allow LaTex formulas.

As workaround to this limitation, when writing your GH pages you can use a service such as this [Equation Editor (EE)](https://codecogs.com/latex/eqneditor.php).

The idea is that, instead of writing LaTex in your page, you write it in the EE, which will in turn allow you you to select one of several output formats. The one you want is “URL encoded”, which is a link to be inserted where you want the formula to appear via the `![](url_here)` tag (image tag).

For instance, if you want this formula to appear:

![](https://latex.codecogs.com/svg.latex?\lim_{x%20\to%200}%20f(x)%20=%208)

You will have to write its LaTex script `\lim_{x \to 0} f(x) = 8` in the EE, select “svg” in the first drop-down menu under the editor, and “URL encoded” at the bottom of the page. A link will appear underneath the last drop-down (“https://latex.codecogs.com/gif.latex?%5Clim_%7Bx%20%5Cto%200%7D%20f%28x%29%20%3D%208”). Copy it inside the image tag:

```
![](https://latex.codecogs.com/svg.latex?%5Clim_%7Bx%20%5Cto%200%7D%20f%28x%29%20%3D%208)
```

It the formula will appear when the markdown file is rendered:

![](https://latex.codecogs.com/svg.latex?%5Clim_%7Bx%20%5Cto%200%7D%20f%28x%29%20%3D%208)

