*Function for an Exponential fit for MATLAB without curve fitting toolbox*

I had some data ponts and I wanted to fit them exponentially...

*I did not have the `proper package'* So I made this goofy function...
This is pretty niche and worked for my specific problem

This function takes two vectors, **x** and **y** then does a polyfit
if the polyfit comes back with an R^2 of > 0.9 then it spits out an error 
if polytfit comes back < 0.9, then it does another polyfit, now using log10(y)
the resulting equation is then solved and turned into an exponential

the function plots your input **x** and **y**, along with the exponential fit line and equation 
