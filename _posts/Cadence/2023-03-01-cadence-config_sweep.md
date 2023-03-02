---
title: Record results as an animation or video for demo
author: xueyong
date: 2023-03-01 11:33:00 +0800
categories: [Tools, Cadence]
tags: [cadence, ADE assembler, config sweep]
math: true
mermaid: true
image:
  src: https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/cadence/config_sweep.png
---

This post is to show how to run simulations with different views simultaneously.


## Title: [Cadence] Run simulations with different views simultaneously
---
# save data as gif
### function
The function of `save_as_fig` is as follows.

According to the usage, uncomment code lines 15~21 and line 32, then run this part. The `out.fig` file is generated.

### Call the function in a loop

Here is an example to call the function in a loop.

```matlab
x = 0:0.01:1;
fig = figure(1);
filename = 'test.gif';
for n = 1:0.5:5
    y = x.^n;
    plot(x,y)
    % save animation as fig
    save_as_gif(n, 1, fig, 0.5, filename);
end
```

The result of `test.fig` is as follows.
![avatar](https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/cadence/config_sweep.png "Config Sweep")


