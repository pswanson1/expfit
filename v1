function [Exp_eq,b] = expfit(x,y)
    arguments
        x (1,:) {mustBeNumeric, mustBeFinite}
        y (1,:) {mustBePositive,mustBeNumeric, mustBeFinite}
    end
    % if inputs no the same size, then error bad idk why they dont
    % have some argument validation for this?
    %
    if ~isequal(size(x),size(y))
        eid = 'Size:notEqual';
        msg = 'Size of first input must equal size of second input.';
        error(eid,msg)
    end
% this function creates a simple exponential fit from
% a series of x,y data points
% the function uses polyfit to create a linear fit ( keeping track of the
% R^2)
% the input data is `turned into logspace':
% \log \left(f(x)\right)=\log \left(a\right)+x\log \left(b\right)
% this equation is then solved and turned into an exponential
% DOES NOT WORK FOR negative VALUES (SORRY)
% ==================================================================
% first, fit the data using polyfit
[P,S] = polyfit(x,log10(y),1);
%example P = -0.4119   40.9924
% y =-0.4119*x+40.9924
%
R_squared = 1 - (S.normr/norm(y - mean(y)))^2;
if R_squared > 0.999
    error('R^2 > 0.999: Line of best fit is linear')
end
%global R_squared
% R^2 equation, not going to talk about this
% but R^2 for use in nonlinear fits is not recommended:
%
% "... almost all of the commercially available statistical software
% packages (i.e. Prism, Origin, Matlab, SPSS, SAS) calculate R^2 values 
% for nonlinear fits, which is bound to unintentionally corroborate its 
% frequent use."
% see: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2892436/
%
%yfit = P(1)*x+P(2);

% solving log10 liner combo
% log10(y) = m*x+b
%rearrange
% y = 10^{m*x+b}
% y = 10^{b}*10^{mx}
% y = 10^{b}*(10^{m})^x
exp_1 = 10^P(2); % = 10^b
exp_2 = 10^P(1); % = 10^m
Exp_eq = string(exp_1)+'*('+string(exp_2)+')^x';
Exp_latex = string(exp_1)+'('+string(exp_2)+')$^x$';
%disp(Exp_eq)
% create a 'continuous looking line' in the output plot
step = (max(x)-min(x))/100; % step for each x-value in the exp graph
exp_x = min(x)-step*length(x):step:max(x)+step*length(x);
% plot the output
hold on 
scatter(x,y) % plot the original x,y data
plot(exp_x,exp_1.*(exp_2.^exp_x)) % plot the new exp fit
eqn = string(" Exp: y = " + Exp_latex); % displat equation
text(min(x),max(y),eqn,"HorizontalAlignment","left","VerticalAlignment","top",'Interpreter','latex')
end
