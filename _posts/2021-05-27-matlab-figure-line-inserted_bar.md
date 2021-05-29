---
title: Insert Histogram into Line Chart
author: xueyong
date: 2021-05-26 11:33:00 +0800
categories: [Tools, Matlab]
tags: [matlab, histogram, bar, Monte Carlo]
math: true
mermaid: true
image:
  src: https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/matlab/tempreture_calibration.png

---

## How To Insert Histogram into Line Chart
---

## Code

```matlab
% insert multiple histograms into line chart
figure;
ax0 = axes('position',[0.1,0.1,0.8,0.8]); 
ax1 = axes('position',[0.175,0.47,0.2,0.15]); 
ax2 = axes('position',[0.175,0.27,0.2,0.15]); 
ax3 = axes('position',[0.425,0.47,0.2,0.15]); 
ax4 = axes('position',[0.425,0.27,0.2,0.15]); 
ax5 = axes('position',[0.675,0.47,0.2,0.15]); 
ax6 = axes('position',[0.675,0.27,0.2,0.15]); 
axes(ax0)
A = importdata('vg_calibration.csv'); % line chart data
x = A.data(:,1);
y = A.data(:,2);
plot(x,y,'d-','LineWidth',2);
% xlim([-80 140]);
% ylim([0.7 0.85]);
xlabel({'Tempreture (\circC)'});
ylabel({'Voltage (V)'});
legend('Gate voltage varies with tempreture','FontName','Times New Roman','FontSize',10);
legend('boxoff');
grid on
hold on;
text(-20,0.805, ...
    {'@T=-40\circC'}, ...
     'FontName','Times New Roman','FontSize',10,'FontWeight','Bold');
text(25,0.805, ...
    {'@T=30\circC'}, ...
     'FontName','Times New Roman','FontSize',10,'FontWeight','Bold');
text(67,0.805, ...
    {'@T=100\circC'}, ...
     'FontName','Times New Roman','FontSize',10,'FontWeight','Bold');

N = 2000;
axes(ax1)
A = importdata('Rmos_calibration.csv'); %histogram data (Monte Cralo results)
MC = A.data(:,7) * 1e-3;
% N = length(MC);
nbins = 8;
h1 = histogram(MC,nbins);
h1.FaceColor = 'c';
hold on;
x = linspace(min(MC)*0.9,max(MC)*1.001,100);
[mu,sigma]=normfit(MC);
f = exp(-(x-mu).^2./(2*sigma^2))./(sigma*sqrt(2*pi)); %probability density function (pdf)
y=f/max(f)*max(h1.Values);
plot(x,y,'LineWidth',1.5)
% xlabel({'R_{ON} (K\Omega)'});
% ylabel({'Count'});
set(gca,'color','none');
text(420,640, ...
    {strcat('\mu=', num2str(mu,'%1.2f')); ...
     strcat('\sigma=', num2str(sigma,'%1.2f')); ...
     strcat('n=', num2str(N,'%1.0f'))}, ...
     'FontName','Times New Roman','FontSize',8);

axes(ax2)
A = importdata('Rmos_calibration.csv');
MC = A.data(:,1) * 1e-3;
% N = length(MC);
nbins = 8;
h1 = histogram(MC,nbins);
h1.FaceColor = 'g';
hold on;
x = linspace(min(MC),max(MC)*1.001,100);
[mu,sigma]=normfit(MC);
f = exp(-(x-mu).^2./(2*sigma^2))./(sigma*sqrt(2*pi)); %probability density function (pdf)
y=f/max(f)*max(h1.Values);
plot(x,y,'LineWidth',1.5)
xlabel({'R_{ON} (K\Omega)'});
% ylabel({'Count'});
set(gca,'color','none');
text(min(MC),1300, ...
    {strcat('\mu=', num2str(mu,'%1.2f')); ...
     strcat('\sigma=', num2str(sigma,'%1.2f')); ...
     strcat('n=', num2str(N,'%1.0f'))}, ...
     'FontName','Times New Roman','FontSize',8);

axes(ax3)
A = importdata('Rmos_calibration.csv');
MC = A.data(1:1982,9) * 1e-3;
% N = length(MC);
nbins = 8;
h3 = histogram(MC,nbins);
h3.FaceColor = 'c';
hold on;
x = linspace(min(MC)*0.9,max(MC)*1.001,100);
[mu,sigma]=normfit(MC);
f = exp(-(x-mu).^2./(2*sigma^2))./(sigma*sqrt(2*pi)); %probability density function (pdf)
y=f/max(f)*max(h3.Values);
plot(x,y,'LineWidth',1.5)
ylim([0, 1000]);
% xlabel({'R_{ON} (K\Omega)'});
% ylabel({'Count'});
set(gca,'color','none');
text(350,640, ...
    {strcat('\mu=', num2str(mu,'%1.2f')); ...
     strcat('\sigma=', num2str(sigma,'%1.2f')); ...
     strcat('n=', num2str(N,'%1.0f'))}, ...
     'FontName','Times New Roman','FontSize',8);

axes(ax4)
A = importdata('Rmos_calibration.csv');
MC = A.data(1:1982,3) * 1e-3;
% N = length(MC);
nbins = 8;
h4 = histogram(MC,nbins);
h4.FaceColor = 'g';
hold on;
x = linspace(min(MC),max(MC)*1.001,100);
[mu,sigma]=normfit(MC);
f = exp(-(x-mu).^2./(2*sigma^2))./(sigma*sqrt(2*pi)); %probability density function (pdf)
y=f/max(f)*max(h4.Values);
plot(x,y,'LineWidth',1.5)
xlabel({'R_{ON} (K\Omega)'});
% ylabel({'Count'});
set(gca,'color','none');
text(min(MC),1300, ...
    {strcat('\mu=', num2str(mu,'%1.2f')); ...
     strcat('\sigma=', num2str(sigma,'%1.2f')); ...
     strcat('n=', num2str(N,'%1.0f'))}, ...
     'FontName','Times New Roman','FontSize',8);

axes(ax5)
A = importdata('Rmos_calibration.csv');
MC = A.data(1:1969,11) * 1e-3;
% N = length(MC);
nbins = 8;
h5 = histogram(MC,nbins);
h5.FaceColor = 'c';
legend('MOS resistance distribution w/o calibration','FontName','Times New Roman','FontSize',10);
legend('boxoff');
hold on;
x = linspace(min(MC)*0.9,max(MC)*1.001,100);
[mu,sigma]=normfit(MC);
f = exp(-(x-mu).^2./(2*sigma^2))./(sigma*sqrt(2*pi)); %probability density function (pdf)
y=f/max(f)*max(h5.Values);
plot(x,y,'LineWidth',1.5)
xlim([150 420]);
ylim([0, 1000]);
% xlabel({'R_{ON} (K\Omega)'});
% ylabel({'Count'});
set(gca,'color','none');
text(300,640, ...
    {strcat('\mu=', num2str(mu,'%1.2f')); ...
     strcat('\sigma=', num2str(sigma,'%1.2f')); ...
     strcat('n=', num2str(N,'%1.0f'))}, ...
     'FontName','Times New Roman','FontSize',8);

axes(ax6)
A = importdata('Rmos_calibration.csv');
MC = A.data(1:1969,5) * 1e-3;
% N = length(MC);
nbins = 8;
h6 = histogram(MC,nbins);
h6.FaceColor = 'g';
legend('MOS resistance distribution w/ calibration','FontName','Times New Roman','FontSize',10);
legend('boxoff');
hold on;
x = linspace(min(MC),max(MC)*1.001,100);
[mu,sigma]=normfit(MC);
f = exp(-(x-mu).^2./(2*sigma^2))./(sigma*sqrt(2*pi)); %probability density function (pdf)
y=f/max(f)*max(h6.Values);
plot(x,y,'LineWidth',1.5)
ylim([0, 2000])
xlabel({'R_{ON} (K\Omega)'});
% ylabel({'Count'});
set(gca,'color','none');
text(min(MC),1300, ...
    {strcat('\mu=', num2str(mu,'%1.2f')); ...
     strcat('\sigma=', num2str(sigma,'%1.2f')); ...
     strcat('n=', num2str(N,'%1.0f'))}, ...
     'FontName','Times New Roman','FontSize',8);

% axes(ax0)
% set(gca,'color','none');
% legend([h5],'MOS resistance distribution w/o calibration');
% legend([h6],'MOS resistance distribution w/ calibration');
% legend('boxoff')
% legend([h3 h4],...
%      {'MOS resistance distribution w/o calibration',...
%       'MOS resistance distribution w/ calibration'},...
%       'Location','northoutside')

```

Need modify the legends manually.

## Result

![histogram](https://raw.githubusercontent.com/ntuzxy/ntuzxy.github.io/master/figs/matlab/tempreture_calibration.png "Histograms inserted into line chart"){: width=50%}
_Histograms inserted into line chart_
