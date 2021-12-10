---
title: TESTING
author: xueyong
date: 2021-04-27 11:33:00 +0800
categories: [Tools, Matlab]
tags: [matlab, ledgend, loop]
math: true
mermaid: true
image:
  src: https://cdn.jsdelivr.net/gh/cotes2020/chirpy-images/commons/devices-mockup.png
---


## Titles
---
# H1 - heading

<h2 data-toc-skip>H2 - heading</h2>

<h3 data-toc-skip>H3 - heading</h3>

<h4>H4 - heading</h4>
---
<br>

```matlab
% clear;clc;
i=0; % for legend_str
figure('name','plot in loops')
LineStyle = '-';
Marker = 'o+*.x';
color = 'rgbkm'; 
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
                'Color',color(mod(i,5)+1)); 
            hold on; 
            i=i+1;
            legend_str{i} = ['K=', num2str(m), ',N=', num2str(n),',K=', num2str(k)];
        end
    end
end
legend(legend_str);
```

## Paragraph
