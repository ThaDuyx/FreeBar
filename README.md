# FreeBar
> Mini project for the '[Physical Modelling for Sound Synthesis](https://moduler.aau.dk/course/2023-2024/MSNSMCM2175)' course @AAU, Cph 2023/2024

This is an implementation of the damped ideal bar equation with free boundary conditions.
## Ideal Bar

If we want to model the physical properties of a marimba the easiest way to go about it is using the ideal bar equation.
The partial differential equation(PDE) of the Ideal bar is the following:
$$\partial^2_t=-\kappa^2\partial^4_xu$$
and discretised to the finite difference scheme(FD):
$$\delta_{tt}u^n_l=-\kappa^2\delta_{xxxx}u^n_l$$

## Damping
In order to model the physics of an actual marimba we also have to add an expression which accounts for the energy loss in the system. 
This is done by adding the damping term. The expression for damping is given by:
$$-2\sigma_0\partial_tu+2\sigma_1\partial_t\partial^2_xu$$

Where loss of energy is accounted for with the $\sigma_0$ expression, and the frequency dependant damping is accounted for with the $\sigma_1$ expression. This expands the expression of the ideal bar equation with the following continuous PDE:
$$\rho A\partial^2_tu=-EI\partial^4_xu-2\sigma_0\partial_tu+2\sigma_1\partial_t\partial^2_x u$$
and discretised to the FD scheme:

$$\rho A \delta_{tt}u^n_l=-EI\delta_{xxxx}u^n_l-2\sigma_0\delta_tu^n_l+2\sigma_1\delta_t\delta_{xx}u^n_l$$

## Expansions
We can use finite difference operators to make approximations to the PDE’s derivatives. 
To generate an explicit finite difference scheme we’ll use a centred time difference approximation for the $\sigma_0$ expression. 
For the mixed derivative in the $\sigma_1$ expression the backward time difference will be used for the temporal
derivative.


## Boundary conditions
