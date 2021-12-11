---
title: Matlab Plot Settings
author: xueyong
date: 2021-12-10 11:33:00 +0800
categories: [Tools, Matlab]
tags: [matlab, plot, settings, paper]
math: true
mermaid: true
image:
  src: https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/matlab/matlab_plot_settings.png
---

可以用于paper的图片设置
## Code
```matlab
% This is from startup.m (on website)
% Plot formattingcolordef white;
% Plot with default font size 16+
% Linewidth of 2 or 3
set(0,'defaultAxesFontName', 'Arial', ...
    'defaultTextFontName', 'Arial', ...
    'defaultAxesFontWeight', 'Bold', ...
    'defaultTextFontWeight', 'Bold', ...
    'DefaultTextFontSize', 16, ...
    'DefaultAxesFontSize', 16, ...
    'DefaultLineLineWidth', 3.0, ...
    'DefaultAxesLineWidth', 3, ...
    'DefaultPatchLineWidth', 2, ...
    'DefaultAxesXGrid', 'on', ...
    'DefaultAxesYGrid', 'on');

% Loading/plotting data
% data = csvread('nmos_iv_data.csv', 1);
data = [1:9; 1:9]';
voltage = data(:,1);
current = data(:,2)*1e6;
plot(voltage, current);

xlabel('Voltage [V]');
ylabel('Current [uA]');
title('NMOS IV Curve');
```


显示效果如下：
<center><embed src="https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/matlab/matlab_plot_settings.pdf" width="850" height="600"></center>

![](https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/matlab/matlab_plot_settings.png)






