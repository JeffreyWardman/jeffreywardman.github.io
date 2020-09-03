---
title: "An Analysis of the Effect of Deformations on the Performance of NACA2412 Airfoils with an Angle of Attack of 5"
published: true
---

<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

# Optimal Angle of Attack and Effect of Deformations on the Performance of NACA2412 Airfoils with an AoA of 5

The NACA2412 airfoil was analysed through XFOIL and MATLAB to identify the effect of the angle of attack on the lift-to-drag (L/D) ratio with a Mach number of 0.1 and Reynolds number of $$10^7$$. The Monte Carlo method was used to identify the optimum L/D ratio caused by deformations of the airfoil with an angle of attack of 5 degrees. Sample sizes of 100, 1000 and 10,000 were used. This theoretical data was compared to experimental data obtained in a wind tunnel to identify the accuracy of the modelling. After 10,000 samples, the most efficient formation of the airfoil was between 124.0 and 124.5 with top and bottom deformations of approximately -0.0025 and 0.0050 respectively.

# Introduction

The NACA2412 airfoil is a two-dimensional body that moves through fluid to generate aerodynamic forces and is used as an airfoil shape for aircraft wings. It has a maximum camber of 2% at its 40% chord point (40% from the leading edge) and a maximum thickness of 12% of its chord length (Brandt _et al._ 1959). The curvature of the body causes the velocity of the wind to differ on the top and bottom of the structure which causes lift and drag (Brandt _et al._). Lift is the component of the aerodynamic force that is perpendicular to the velocity vector, whereas the drag force is that which is parallel (Brandt _et al._).

The Monte Carlo method relies on repeated simulations based on random sampling to generate numerical results. It can be used to sample different lift-to-drag (L/D) ratios caused by varying the deformation or angle of attack of the NACA2412 airfoil. This process can be executed with XFOIL – a program that simulates the effect of different variables on airfoils. This program can be used via MATLAB to run multiple samples with minimal input through loops. However, the MATLAB wrapper is limited by its poor modelling of stalling. Therefore, there can only be small values of the angle of attack when analysing the effects of deformation on the airfoil. This stalling effect is represented in the L/D ratio when there is a sudden drop as the angle of attack increases. It can be explained by the separation of the flow in the boundary layer caused by the negative pressure gradient. This gradient causes the sheer stress to become negative and a region of recirculating flow that does not follow the contour of the body occurs – i.e. the separation of flow from the body of the airfoil (McCullough _et al._ 1951). If this occurs near the leading edge (as at high angles), the flow may not reattach but merge with the wake instead (McCullough _et al._). This causes the airfoil to rapidly lose lift at high angles to the flow (McCullough _et al._).

The Mach number (Ma) was set to 0.1 for the analysis. This is defined as:

$$
\text{Ma} = \frac{u}{c}
$$

where $$u$$ is the flow velocity past a boundary and $$c$$ is the speed of sound in the medium. If Ma is less than one, the flow velocity is less than the speed of sound.
The Reynolds number was set to $$10^7$$ for analysis. It represents the type of flow in the body and is defined as:

$$
\text{Re} = \frac{\rho u L}{\mu} = \frac{uL}{v}
$$

where:

- $$\rho$$ is the fluid density [kg/m$$^3$$]
- $$u$$ is the flow speed [m/s]
- $$L$$ is the length of the body [m]
- $$\mu$$ is the dynamic viscosity of the fluid [kg/(ms)]
- $$v$$ is the kinetic viscosity of the fluid [m$$^2$$/s]

This blog post investigates the effect of a change of the angle of attack on the lift, drag and lift-to-drag ratio when using a Mach number of 0.1 and Reynolds number of $$10^7$$. It also seeks to find the largest lift-to-drag ratio caused by different values of deformation of an NACA2412 airfoil with an angle of attack of 5 degrees. A large ratio identifies a more energy efficient model and thus, the optimal model will be that with the highest ratio achieved.

# Methodology

The optimal performance of the NACA2412 airfoil was determined by the following tasks:

1. Identify the effect of changing the angle of attack from 0 to 16 degrees in increments of 1 degree on the lift, drag and L/D ratio. The deformation of the airfoil was kept constant during this process.

2. Compare these theoretical values to the experimental data obtained from wind tunnel trials supplied by Abbott and Doenhoff (1959).

3. Identify the effect of deforming the airfoil by adding deformations of the form [a b].

4. Apply Monte Carlo sampling with samples of 100, 1000 and 10,000 to represent the raw data given for the lift and drag coefficients when deformation was randomly sampled between -0.025 and 0.025. During this process, the angle of attack was kept constant at 5 degrees.

# Results & Discussion

The results of Task 1 are represented in Figure 1. The optimal L/D ratio is at an angle of attack of 9 degrees. It is observed that a linear relationship exists between the lift coefficient and the angle of attack of the NACA2412 airfoil for low angles of attack. This relationship begins to falter after an angle of attack of 10 degrees, which can be seen in Figure 2, with the experimental results. This stalling is not obvious in the results obtained from the simulations and shows a decline in accuracy for large values for the angle of attack.

It was identified that an exponential relationship between the drag and angle of attack existed. This makes sense due to the separation of flow that magnifies the effect of drag as the angle of attack increases.

Figure 3 shows that the theoretical L/D ratios for Task 2 were consistently larger than that of the experimental data. This, alongside Table 1. Show that the optimal angle of attack was different between the two types of data. The optimal L/D ratio for the experimental data occurred at 6 degrees (66.7) whereas it occurred at an angle of attack of 9 degrees for the results produced (136). The value of 9 degrees is close to the stalling angle of the NACA2412 airfoil and thus, may be inaccurate. This conclusion is reinforced by the lower optimum angle of attack for the experimental data.

{: style="text-align:center"}
![](/assets/posts/airfoil-analysis/polar_ld_aoa.png)

<sup>Figure 1. Polar of the lift and drag as a function of the angle of attack. $$C_l$$ and $$C_d$$ are the lift and drag coefficients. CFD is the computational fluid dynamics of the body and shows the effectiveness of the airfoil body. $$C_d$$ is approximately 100 times smaller than $$C_l$$.</sup>

<sup>Table 1. A comparison of the theoretical lift-to-drag ratio to that of a previous experimental study for different angles of attack. Theoretical data was obtained from the MATLAB code (see appendix) and experimental data was obtained from _Theory of Wing Sections_ (Abbott & Von Doenhoff 1959).</sup>

| Angle of attack (degrees) | Theoretial lift coefficient | Theoretical drag coefficient | Theoretical L/D ratio | Experimental lift coefficient | Experimental drag coefficient | Experimental L/D Ratio |
| :-----------------------: | :-------------------------: | :--------------------------: | :-------------------: | :---------------------------: | :---------------------------: | :--------------------: |
|             0             |           0.2384            |           0.00505            |         47.2          |              0.2              |             0.098             |          2.04          |
|             1             |           0.3460            |           0.00507            |         68.2          |               -               |               -               |           -            |
|             2             |           0.4501            |           0.00521            |         86.4          |              0.4              |             0.01              |          40.0          |
|             3             |           0.5518            |           0.00541            |          102          |               -               |               -               |           -            |
|             4             |           0.6513            |           0.00581            |          112          |            0.6125             |             0.011             |          55.7          |
|             5             |           0.7481            |           0.00618            |          121          |               -               |               -               |           -            |
|             6             |           0.8404            |           0.00649            |          129          |              0.8              |             0.012             |          66.7          |
|             7             |           0.9925            |           0.00739            |          134          |               -               |               -               |           -            |
|             8             |           1.1105            |           0.00818            |          136          |               1               |             0.017             |          58.8          |
|             9             |           1.2296            |           0.00902            |          136          |               -               |               -               |           -            |
|            10             |           1.3299            |           0.00991            |          134          |             1.16              |            0.0225             |          51.6          |
|            11             |           1.4118            |           0.01082            |         130.5         |               -               |               -               |           -            |
|            12             |           1.4956            |           0.01185            |         126.2         |              1.2              |               -               |           -            |
|            13             |           1.5663            |           0.01309            |         119.7         |               -               |               -               |           -            |
|            14             |           1.6351            |           0.01446            |         113.1         |             1.21              |               -               |           -            |
|            15             |           1.6955            |           0.01642            |         103.4         |               -               |               -               |           -            |
|            16             |           1.7526            |           0.01875            |         93.47         |             0.75              |             0.013             |          57.7          |

{: style="text-align:center"}
![](/assets/posts/airfoil-analysis/lift_coefficient.png)

<sup>Figure 2. A comparison of the theoretical lift coefficient to that of a previous experimental study for different angles of attack. Theoretical data was obtained from the MATLAB code (see appendix) and experimental data was obtained from _Theory of Wing Sections_ (Abbott & Von Doenhoff 1959).</sup>

{: style="text-align:center"}
![](/assets/posts/airfoil-analysis/ld_ratio.png)

<sup>Figure 3. A comparison of the theoretical L/D ratio to that of a previous experimental study for different angles of attack. Theoretical data was obtained from the MATLAB code (see appendix) and experimental data was obtained from _Theory of Wing Sections_ (Abbott & Von Doenhoff 1959). Data missing from experimental results.</sup>

Figure 4 below shows the effect of the deformations of an airfoil from above and below. It can be seen that the matrix [a b] increases the thickness of the airfoil by deforming the top (a) and bottom (b) independently.

{: style="text-align:center"}
![](/assets/posts/airfoil-analysis/def_0.png) ![](/assets/posts/airfoil-analysis/def_1.png) ![](/assets/posts/airfoil-analysis/def_2.png)
![](/assets/posts/airfoil-analysis/def_3.png) ![](/assets/posts/airfoil-analysis/def_4.png) ![](/assets/posts/airfoil-analysis/def_5.png)

<sup>Figure 4. Deformations of the form [a b] of a NACA2142 airfoi with an angle of attack of 5 degrees. $a$, $b$ are combinations of 0, 0.05, 0.10.</sup>

The Monte Carlo method is displayed in Figure 5. below. It shows the random sampling of deformations between -0.025 and 0.025 for the NACA2412 airfoil. 100, 1,000 and 10,000 samples were used to identify the optimal deformation with increasing accuracy. The scatterplot formed by this simulation shows the effect of different values of deformation to the top and bottom of the airfoil on the L/D ratio. It can be seen in the figure that the highest values of the ratio occur when both forms of deformation approach 0.

{: style="text-align:center"}
![](/assets/posts/airfoil-analysis/sampling_100.png) ![](/assets/posts/airfoil-analysis/sampling_1000.png) ![](/assets/posts/airfoil-analysis/sampling_10000.png)

<sup>Figure 5. Raw Monte Carlo results of a NACA2142 airfoil with 100, 1000, 10,000, samples.</sup>

Table 2 highlights that the mean optimal ratio was at $$115.41 \pm 4.8202$$ with 10,000 samples. Interestingly, this was slightly lower in variety than the 1000 samples which had the result of $$115.49 \pm 4.7883$$.

Figure 6 shows that the step size of both the optimum L/D ratio and its respective deformation decreased with the increase in sample size. This shows that the accuracy improved as sample size increased and is a visualisation of the effectiveness of the Monte Carlo method. With 10,000 samples, the optimal L/D ratio is between 124.0 and 124.5 and occurs when the deformation at the top is approximately -0.0025 whilst the bottom is slightly lower than 0.0050. This is not the case with lower samples. 100 samples indicate a ratio between 123.5 and 124.0 with deformations of approximately -0.0050 and 0.0025 for top and bottom respectively. Lastly, 1000 samples suggest a ratio slightly larger than 124.0 with top and bottom deformations of approximately -0.0050 and 0.0050 respectively.

<sup>Table 2. Reference and mean L/D ratio and standard deviations for different number of iterations of the Monte Carlo method for different deformations between -0.025 and 0.025 and constant angle of attack of 5 degrees for an NACA2412 airfoil.</sup>

| $$\frac{\text{Number}}{\text{of iterations}}$$ | $$\frac{\text{Reference}}{\text{L/D ratio}}$$ | $$\frac{\text{Mean optimal}}{\text{L/D ratio}}$$ | $$\frac{\text{Standard deviation}}{\text{of L/D ratio}}$$ |
| :--------------------------------------------: | :-------------------------------------------: | :----------------------------------------------: | :-------------------------------------------------------: |
|                      100                       |                    121.05                     |                      114.60                      |                          5.3653                           |
|                      1000                      |                    121.05                     |                      115.49                      |                          4.7883                           |
|                     10,000                     |                    121.05                     |                      115.41                      |                          4.8202                           |

{: style="text-align:center"}
![](/assets/posts/airfoil-analysis/lift_to_drag_100.png) ![](/assets/posts/airfoil-analysis/deformation_100.png)

{: style="text-align:center"}
![](/assets/posts/airfoil-analysis/lift_to_drag_1000.png) ![](/assets/posts/airfoil-analysis/deformation_1000.png)

{: style="text-align:center"}
![](/assets/posts/airfoil-analysis/lift_to_drag_10000.png) ![](/assets/posts/airfoil-analysis/deformation_10000.png)

<sup>Figure 6. Monte Carlo convergence of the optimum L/D ratio and its respective deformation of the top and bottom of a NACA2142 airfoil with 100, 1000, 10,000, samples. $$C_l$$ and $$C_d$$ are the lift and drag coefficients.</sup>

# Conclusion

The Monte Carlo sampling method was used to identify the ideal deformation of the NACA2412 airfoil with angle of attack of 5 degrees, Mach number 0.1 and Reynolds number $$10^7$$. After 10,000 samples, it was identified that the most efficient formation of the airfoil was between 124.0 and 124.5 with top and bottom deformations of approximately -0.0025 and 0.0050 respectively. Comparing these results to the optimal L/D ratio of different angles of attack such as that at the theoretically optimal 9 degrees would help determine whether 9 degrees or another value is the optimal angle of attack. The limitations of MATLAB and XFOIL as the angle of attack increased was a flaw that would need to be resolved to more accurately identify the optimal deformations of the NACA2412 airfoil.

# Acknowledgements

MATLAB and XFOIL were used to develop a theoretical model for NACA2412 aerofoils.

Experimental data was developed by Abbott & Doenhoff (1959).

# References

1. S.A. Brandt, R.J. Stiles, J.J. Bertin and R. Whitford, Introduction to Aeronautics: A Design Perspective (American Insititute of Aeronautics and Astronautics, Inc., Reston, 1959), pp. 94-124.

2. G.B. McCullough and D.E. Gault, Examples of Three Representative Types of Airfoil-section Stall at Low Speed (NACA, Washington, 1951).

3. I.H. Abbott and A.E. Von Doenhoff, Theory of Wing Sections (Dover Publications, Inc., New York, 1959), pp. 482–483.

# Code

```
%% Preliminaries
clc % clear the command window
clear % clear the workspace
close all % close all figures

% Add the directory /xfoil/ to the searchpath
addpath xfoil

%% General Settings
designation = '2412'; % Use a NACA 2412 airfoil
reynolds = 10e7; % Reynold's number
mach = 0.1; % Mach number

%% Setting up XFOIL on MATLAB
% Run XFOIL from MATLAB using the function runXFOIL.

% == Local Settings ==
deformation = [0 0];
aoa = 5;  % Angle of Attack

% == Run CFD Solver ==
[cl,cd] = runXFOIL(designation,deformation,aoa,reynolds,mach);

% == Print Output to Command Window ==
table(aoa,cl,cd)

%% Task 1
% Plot of the lift and drag, as a function of the angle of attack.
% == Local Settings ==
deformation = [0 0];
aoa = linspace(0,16,17)';

% == Pre-Allocate ==
cl = nan(size(aoa));
cd = nan(size(aoa));

% == Run CFD Solver ==
for k = 1:length(aoa)
    [cl(k),cd(k)] = runXFOIL(designation,deformation,aoa(k),reynolds,mach);
end

% == Print Output to Command Window ==
table(aoa,cl,cd)

% == Plot Results ==
figure()
plot(aoa,cl,'bo-',aoa,100*cd,'rs-',aoa,cl./cd/100,'go-')
xlabel('Angle of Attack')
ylabel('CFD result')
legend('C_l','100 \times C_d','0.01 \times C_l/C_d','location','northwest')
title('Task 3: Polar of the lift and drag, as a function of the angle of attack')

%% Plot a deformed airfoil.
% == Local Settings ==
deformation = [0.05 0];

% == Plot Shape ==
figure()
h1 = plotNACA4deformed(designation,[0 0],'k'); % plot the undeformed shape

hold on
h2 = plotNACA4deformed(designation,deformation,'r'); % plot the deformed shape
hold off

axis equal
xlabel('x')
ylabel('y')
legend([h1(1) h2(1)],'Baseline','Deformed')
title('Task 3: [0.05, 0] deformation of NACA2142 airfoil')

%% Run a Monte Carlo simulation.
% local settings
aoa = 5;
nmc = 100; % Change between 100, 1000, 10000
defMag = 0.025;
rng(1) % Set random number generator seed for analysis

% create random samples
deformation = -defMag + 2*defMag*rand(nmc,2);

% run the CFD solver for the undeformed airfoil (this will provide a
% reference lift-to-drag ratio l2d_0 )
[cl,cd] = runXFOIL(designation,[0 0],aoa,reynolds,mach);
l2d_0 = cl/cd;

% pre-allocate the lift-to-drag ratio
l2d = nan(nmc,1);

% run the CFD solver for each sample, and store the lift-to-drag ratio
for k = 1:nmc
    [cl,cd] = runXFOIL(designation,deformation(k,:),aoa,reynolds,mach);
    l2d(k) = cl/cd;
end

% plot CFD output
figure()
scatter(deformation(:,1),deformation(:,2),30,l2d,'filled')
h = colorbar;
xlabel('Deformation on top')
ylabel('Deformation on bottom')
ylabel(h,'C_l / C_d')
title('Task 4: Raw Monte Carlo results with 100 samples')

% Monte Carlo analysis
l2d_Mean = mean(l2d);
l2d_Std = std(l2d);
table(l2d_0,l2d_Mean,l2d_Std)

%% Plot the convergence of the optimum
% i.e. plot the maximum lift-to-drag ratio and the corresponding
% shape deformation as a function of the number of random samples.

l2d_max = nan(size(l2d));
def_max = nan(size(deformation));

for k = 1:nmc
   [l2d_max(k),id] = max(l2d(1:k));
   def_max(k,:) = deformation(id,:);
end

figure()
semilogx(l2d_max,'b-')
xlabel('# Simulations')
ylabel('Maximum C_l / C_d')
title('Task 5: Monte Carlo convergence of the lift-to-drag ratio for 100 samples')

figure()
semilogx(def_max,'-')
xlabel('# Simulations')
ylabel('Deformation_{max}')
title('Task 6: Monte Carlo convergence of the deformation for 100 samples')
legend('Top','Bottom')
```
