---
title: Statistical analysis -- Boxplot
author: xueyong
date: 2021-04-26 11:33:00 +0800
categories: [Tools, Matlab]
tags: [matlab, boxplot, statistics, distribution] # TAG names should always be lowercase
toc: true
comments: true
math: true
mermaid: true
image:
  src: https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/matlab/matlab_boxplot.png

---

# code

```matlab
% import data
A = importdata('cap_sweep.csv');
v = A.data(:,1);
c = A.data(:,4).*1e15;
figure
boxplot(c,v);   % sample boxplot with grouping
hAx=gca;        % retrieve the axes handle
xtk=hAx.XTick;  % and the xtick values to plot() at...
% vg = 0:0.1:1.2;
% xtick = sprintfc('%g',vg);
% xticklabels(xtick);
hold on
cc = zeros(2000,13);
for n = 1:1:13
   cc(1:2000,n) = c((n-1)*2000+1:n*2000);
end
line(xtk,mean(cc))
% line(xtk,mean(cc),'Color','red','LineStyle','--')

xlabel('Vg (V)');
ylabel('Cg (fF)');
set(gca,'FontName','Arial','FontWeight', 'Bold','FontSize',12);



% #### Subfigure: histogram
% import data
A = importdata('cap.csv');
c = A.data(:,3)*1e15;

hold on
axes('position',[0.55,0.25,0.3,0.35]); 
nbins = 9;
h1=histogram(c,nbins);
hold on
x = 3.55:0.001:3.65;
[mu,sigma]=normfit(c);
f = exp(-(x-mu).^2./(2*sigma^2))./(sigma*sqrt(2*pi));
y=f/max(f)*max(h1.Values);
plot(x,y,'LineWidth',1.5)
xlabel('Cg (fF)');
ylabel('No. of occurences');
title('@Vg=1.2V')
set(gca,'FontName','Arial','FontWeight', 'Bold','FontSize',10);
text(3.623,450, ...
    {strcat('\mu=', num2str(mu,'%1.2f')); ...
     strcat('\sigma=', num2str(sigma,'%1.2f')); ...
     strcat('n=', num2str(2000))}, ...
     'FontName','Arial','FontSize',10);![image](https://user-images.githubusercontent.com/34510137/178109784-d0a2b01a-7854-464c-91db-562f48103d15.png)
```

# result

![avatar](https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/matlab/matlab_boxplot.png "Boxplot")
_Legend Generation_
