---
title: Import data from cadence to matlab
author: xueyong
date: 2021-04-26 11:33:00 +0800
categories: [Tools, Matlab]
tags: [matlab, cadence, excel, data processing]
math: true
mermaid: true
image:
---

# Export data from cadence
In ADE window, Tools -> Results Browser. 
Go to ViVA window, select signals and hit right mouse button. 
![avatar](https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/matlab/cadence_export_data_as_excel.png "Export As Excel")

# Import data to matlab

```matlab
clear;clc;
path = '/home/Div6/research/zhangray16/sim_results/diffusion';
A = importdata('diffusion_32x24_4x4_0_900mV.csv');
% A = importdata('diffusion_32x24_16x8.csv');
D = A.data;
[N,M] = size(D);
Data = D(2:N,2:M);
Time = D(2:N,1);
[N,M] = size(Data);
```
