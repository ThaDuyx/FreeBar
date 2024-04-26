# FreeBar
> Mini project for the '[Physical Modelling for Sound Synthesis](https://moduler.aau.dk/course/2023-2024/MSNSMCM2175)' course @AAU, Cph 2023/2024

This is an implementation of the damped ideal bar equation with free boundary conditions.
## Ideal Bar

If we want to model the physical properties of a marimba the easiest way to go about it is using the ideal bar equation.
The partial differential equation(PDE) of the Ideal bar is the following:
$$\partial^2_t=-\kappa^2\partial^4_xu$$
and discretised to the finite difference scheme(FD):
$$\delta_{tt}u^n_l=-\kappa^2\delta_{xxxx}u^n_l$$
