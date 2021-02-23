---
title: Record results as a video for demo
author: xueyong
date: 2021-02-23 11:33:00 +0800
categories: [Blogging, Tutorial, Matlab]
tags: [matlab, video, gif, avi]
math: true
mermaid: true
image:
  src: https://cdn.jsdelivr.net/gh/cotes2020/chirpy-images/commons/devices-mockup.png
---

This post is to show Markdown syntax rendering on [**Chirpy**](https://github.com/cotes2020/jekyll-theme-chirpy/fork), you can also use it as an example of writing. Now, let's start looking at text and typography.


## Titles
---
# H1 - heading

<h2 data-toc-skip>H2 - heading</h2>

<h3 data-toc-skip>H3 - heading</h3>

<h4>H4 - heading</h4>
---
<br>

## Paragraph

I wandered lonely as a cloud

That floats on high o'er vales and hills,

When all at once I saw a crowd,

```matlab
function save_as_gif(i, i0, fig, tpf, filename)
	%%%% this function is to save figure as a gif file
	%%%% put this function in a loop where i is the index
	%%%% i: index of the loop
	%%%% i0: initial value of i
	%%%% fig: the handle of figure
	%%%% tpf: time duration per frame if there is no other delay in the loop, e.g. 0.3
	%%%% filename: filename to be saved, e.g. 'mygif.gif'
	
	% fig = figure;
	% subplot(1, 2, 1);
	% subplot(1, 2, 2);
	frame = getframe(fig);
	
	im=frame2im(frame);
	[I,map]=rgb2ind(im, 256);
	if i == i0;
	    imwrite(I, map, filename, 'gif', 'Loopcount', Inf, 'DelayTime', tpf);%其中Loopcount设置为Inf可以让这个动画无限播放下去
	else
	    imwrite(I, map, filename, 'gif', 'WriteMode', 'append', 'DelayTime', tpf);
end
```


