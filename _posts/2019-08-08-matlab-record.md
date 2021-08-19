---
title: Record results as an animation or video for demo
author: xueyong
date: 2021-02-23 11:33:00 +0800
categories: [Tools, Matlab]
tags: [matlab, animation, video, gif, avi]
math: true
mermaid: true
image:
  src: https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/matlab/save_as_gif.gif
---

This post is to show how to record results as animation or video using Matlab.


## Title: Record results as an animation or video for demonstration
---
### function
The function of ``save_as_fig" is as follows.

```matlab
function save_as_gif(i, i0, fig, tpf, filename)
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%% Author: Xueyong
%%%% Date: 2020-05-04
%%%% This function is to save figure as a gif file
%%%% Put this function in a loop where i is the index
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%% i: index of the loop
%%%% i0: initial value of i
%%%% fig: the handle of figure
%%%% tpf: time duration per frame if there is no other delay in the loop, e.g. 0.3
%%%% filename: filename to be saved, e.g. 'mygif.gif'

    %% usage: uncomment the following lines and run this part
    % i0 = 1;
    % fig = figure;
    % tpf = 0.5;
    % filename = 'out.gif';
    % for i = 1:10
        % plot(i,i^2,'.'); hold on;
        % axis([1,10,1,100]);

        frame = getframe(fig);
        im=frame2im(frame);
        [I,map]=rgb2ind(im, 256);
        if i == i0
            imwrite(I, map, filename, 'gif', 'LoopCount', Inf, 'DelayTime', tpf);%LoopCount=Inf, means continuous loop; LoopCount=0, the animation plays once.
        else
            imwrite(I, map, filename, 'gif', 'WriteMode', 'append', 'DelayTime', tpf);
        end

    % end
```

According to the usage, uncomment code lines 15~21 and line 32, then run this part. The "out.fig" file is generated.

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

The result of "test.fig" is as follows.
![avatar](https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/matlab/save_as_gif_test.gif "Save As GIF")



# save data as video

```matlab
% put this block ahead of the loop
fig = figure;
writerObj = VideoWriter('out.avi');	%// create video file
writerObj.FrameRate = 2;            %// set to 2 frames per second
open(writerObj);                    %// open file for writing video data

for i = 1:10
    plot(i,i^2,'.'); hold on;
    axis([1,10,1,100]);

    % put this block in the loop
    frame = getframe(fig);          %// Capture axes or figure as movie frame
    writeVideo(writerObj,frame); 	%// Write video data to file
end

% put this at the end of the loop
close(writerObj);                   %// Close video file
```

The result of "out.avi" is as follows.
![avatar](https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/matlab/save_as_avi.avi "Save As AVI")
