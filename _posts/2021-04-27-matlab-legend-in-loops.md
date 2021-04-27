---
title: Generate Legends for Figures Plotted in Loops
author: xueyong
date: 2021-04-26 11:33:00 +0800
categories: [Tools, Matlab]
tags: [matlab, ledgend, loop]
math: true
mermaid: true
image:
  src: https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/matlab/matlab_legend_loop.png

---

## How To Generate Legends for Figures Plotted in Loops
---

## Code

```matlab
% clear;clc;
i = 0; % for legend_str
figure('name','plot in loops')
LineStyle = '-';
Marker = 'o+*.x';
Color = 'rgbkm'; 
% condition loop
for m = 3:2:7
    for n = 4:2:8
        for k = 8:2:10
            % data
            x = 0:1:9;
            y = m*n*k*x;
            %plot
            plot(x,y,...
                'LineWidth',m*0.5, ...
                'Marker',Marker(mod(i,5)+1),...
                'Color',Color(mod(i,5)+1)); 
            hold on; 
            i=i+1;
            legend_str{i} = ['M=', num2str(m), ',N=', num2str(n), ',K=', num2str(k)];
        end
    end
end
legend(legend_str);
```

## Result

![avatar](https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/matlab/matlab_legend_loop.png "Legend Generation")

![x](https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/matlab/matlab_legend_loop.png){: width="600"}
_Legend Generation_
