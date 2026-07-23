# Track B — Fluid Dynamics / Navier–Stokes: Sparse-Sensor Data Assimilation with a PINN

This project uses a Physics-Informed Neural Network to reconstruct the full velocity (u, v) and
pressure (p) fields of a 2D unsteady incompressible flow from a small number of sparse,
velocity-only sensor measurements. The network is trained with a combined loss: a data-fitting
term at the sparse sensor locations, and a physics-residual term (continuity + x/y-momentum from
the incompressible Navier–Stokes equations) enforced at dense collocation points throughout the
domain — this physics term is what allows the network to infer the *unobserved* pressure field
purely from the momentum equations. The method is validated against the 2D Taylor–Green vortex,
an exact analytical solution to Navier–Stokes, using 80 sparse velocity sensors, achieving ~16-17%
relative L2 error on velocity and ~40% on pressure. Two follow-up experiments probe the method's
practical limits: a sensor-count sweep (20/40/80/160 sensors) shows accuracy improves sharply up
to ~80 sensors and then plateaus, indicating the physics constraints do most of the reconstruction
work beyond that point; and a noise-robustness sweep (0-10% Gaussian noise on sensor readings)
shows velocity error degrades gently and roughly linearly with noise, while pressure error degrades
much faster — consistent with pressure being inferred indirectly through derivatives of the (now
noisy) velocity field rather than measured directly.
