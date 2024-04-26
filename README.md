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

$$\rho A\delta_{tt}u^n_l=-EI\delta_{xxxx}u^n_l-2\sigma_0\delta_{t.}u^n_l+2\sigma_1\delta_{t-}\delta_{xx}u^n_l$$

Now expansions to each section can be applied for generating the update equation which is able to be implemented. 
The expansions for each section is given by:

$$\delta_{tt}u^n_l=\frac{1}{k^2}(u^{n+1}-2u^n_l+u^{n-1}_l)$$

$$\delta_{xxxx}u^n_l=\frac{1}{h^4}(u^n_{l+2}-4u_{l+1}^n+6u^n_l-4u^n_{l-1}+u^n_{l-2})$$

$$\delta_{t.}u^n_l=\frac{1}{2k}(u^{n+1}_l-u^{n-1}_l)$$

### Mixed derivative
$$\delta_{t-}\delta_{xx}u^n_l$$

A mixed derivative as seen above can be approximated by applying each operator one by one in no specific order. In this case, the backward time difference was applied first to give:
```math
\delta_{t-}\delta_{xx}u^n_l = \frac{1}{k}(\delta_{xx}u^{n}_{l}-\delta_{xx}u^{n-1}_{l})
```


and then the second-order difference in space to:

$$\delta_{t-}\delta_{xx}u^n_l = \frac{1}{k}(\frac{u^{n}_{l+1}-2u^{n}_{l}-2u^{n}_{l+1}}{h^2}-\frac{u^{n-1}_{l+1}-2u^{n-1}_{l}-2u^{n-1}_{l+1}}{h^2})$$

and reduced to:

$$\delta_{t-}\delta_{xx}u^n_l = \frac{1}{kh^2}(u^{n}_{l+1}-2u^{n}_{l}-2u^{n}_{l+1}-u^{n-1}_{l+1}-2u^{n-1}_{l}-2u^{n-1}_{l+1})$$

## Update equation
With the expansions made, these could be substituted into the equation.

$$\rho A\frac{1}{k^2}(u^{n+1}-2u^n_l+u^{n-1}_l)-\frac{EI}{h^4}(u^n_{l+2}-4u_{l+1}^n+6u^n_l-4u^n_{l-1}+u^n_{l-2}) - \frac{2\sigma_0}{k}(u^{n+1}_l-u^{n-1}_l) +\frac{2\sigma_1}{kh^2}(u^{n}_{l+1}-2u^{n}_{l}+u^{n}_{l-1}-u^{n-1}_{l+1}+2u^{n-1}_{l}-u^{n-1}_{l-1})$$




## Boundary conditions
