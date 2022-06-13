# airVelocityAttenuation

This project implements a sink term applicable to the momentum conservation equation of the multiphase OpenFOAM solvers (interFoam, interIsoFoam), which attenuates velocities in the air phase.

## Description

The sink term has the following expression:

$$
\frac{\partial \rho U}{\partial t}+\nabla \cdot \left( \rho U \otimes U \right) -\nabla \cdot \left(2 \rho \nu D \right) + \nabla R_d = -\nabla p + \rho g + \sigma \kappa \nabla \alpha - A_r \rho U  f(\alpha)
$$

where $A_r$ is the attenuation rate (1/s) and $f$ is a function which has a value of zero in the water fraction, and one in the air fraction:

$$
f(\alpha) = \max(\min(\frac{\alpha_t - \alpha}{\alpha_t}, 1), 0)
$$

with $\alpha_t$ being the alpha threshold, bellow which the attenuation is applied.

## Getting Started

* Just copy the `fvOption` file into the `constant` folder of your simulation.
* The attenuation rate and alpha threshold con be easily changed in the source code.

## Example results

![example](https://github.com/esteldunedain/airVelocityAttenuation/blob/master/images/exampleWeir.png?raw=true)

## Warning

* Always ensure that the sink term doesn't affect the problem solution.
* Artifially limiting the air velocity can lead to increased velocity gradients near the free surface, and hence additional turbulence production in that region.

## Author

Nicolás Diego Badano (https://www.linkedin.com/in/nicolas-diego-badano/)
