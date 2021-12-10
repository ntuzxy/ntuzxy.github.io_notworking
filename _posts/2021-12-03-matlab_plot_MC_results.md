---
title: Import MC results from Cadence and Plot using Matlab
author: xueyong
date: 2021-12-03 11:33:00 +0800
categories: [Tools, Matlab]
tags: [matlab, cadence, Monte Carlo, MC, plot]
math: true
mermaid: true
---

---
# 1. Export MC data from Cadence

In ADE result, select `Detail-Transpose`.

`Tools` -> `Export Data`


# 2. Improt data in Matlab and plot MC results 

```matlab
%% improt dat and plot MC results
clear;clc;
addpath('/home/Div6/research/zhangray16/sim_results/DRAM_CIM/4TDRAM_CIM');
filname = 'ExplorerRun_0_transpose.csv';

% preview & read data
opts = detectImportOptions(filname);
preview(filname,opts) %preview data, optional
D = readmatrix(filname);
[N,M] = size(D);
% get interested data
D = D(:,7:8);
[N,M] = size(D);
% separate data
var = 0:100; %sweep range or point in MC simulation
run = 200; %number of runs in MC suimulation
D1 = reshape(D(:,1),run,size(var,2)); %reshape data
D2 = reshape(D(:,2),run,size(var,2));
% replace Nan data with mean value (in case of sim error during MC simulation)
nmean = nanmean(D1); %mean excluding NaN (nanmean function is not recommended)
nmean = mean(D1,'omitnan'); %mean excluding NaN
D1(isnan(D1)) = nmean(ceil(find(isnan(D1))/run));
nmean = mean(D2,'omitnan');
D2(isnan(D2)) = nmean(ceil(find(isnan(D2))/run));

% plot results
figure
plot(var,D1);
hold on;
plot(var,D2);
xlabel({'# of cells'});
ylabel({'BL voltage (V)'});
```

![MC_results](https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/matlab/BL_MC.png "MC_results")
