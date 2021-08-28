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
Go to ViVA window, select signals and hit right mouse button. Select table as follows.
![avatar](https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/cadence/cadence_export_data_as_excel.png "Export As Excel")
In the table window, select File -> Export

# Import data to matlab

## normal simulation data
Normal transient simulation (without corner) data format is like this:

|time |signal1  |signal2  |
|:--: |:--:     |:--:     |
|t1   |s1_value1|s2_value1|
|t2   |s1_value2|s2_value2|
|...  |...      |...      |

Use the following MATLAB code to export the raw data (.csv) to MATLAB.

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
