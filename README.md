pyCOMPASS
=========

This is an effort to rewrite the
[MATLAB COMPASS solver](https://github.com/haraldschilly/compass-solver-matlab)
for the Python ecosystem.

License
-------

Intended to rewrite from scratch and licensed under Apache 2.0

COMPASS MCP Solver
==================

COMPASS is a globally convergent algorithm for solving the Mixed
Complementarity Problem (MCP).
The mathematical theory behind it is based on the PATH solver, the standard
solver for complementarity problems.

COMPASS is an algorithm to solve the mixed complementarity problem (MCP):

    given  f: R^n -> R^n, and (possibly infinite) bounds l, u
    find   z in [l,u], w,v in R_+^n
    s.t.:  f(z) = w-v
           <(z-l),w> = 0
           <(u-z),v> = 0


The MCP in the box constrained formulation (objective function and boundaries)
and the Jacobian of the objective function must be provided in a file
based interface by the user.

COMPASS is an implementation of a stabilized Newton method. The MCP is
reformulated as the problem of finding a zero of a generally nonsmooth
function (normal map, or normal equation), a general first order
approximation of which is computed at the current iterate. Finding a
zero of this approximation turns out to be a linear MCP, which is solved
with the help of a pivot technique, similar to the one described by
Lemke. This pivot algorithm yields a piecewise linear path connecting
the current point and the zero of the approximation.  Whether the
endpoint of this path is accepted as the next iterate, depends on the
non-monotone stabilization (NMS) - scheme, which employs a watchdog
technique: the algorithm is embedded in a general descent framework,
which uses a smooth merit function, and, depending on it, non-monotone
descent criteria. These criteria are not checked in every step, which
reduces the number of function and gradient evaluations. If the solution
to the linear MCP is checked and not accepted, the generated path is
searched for an acceptable point. If no satisfying point can be found,
a projected gradient step is used.

The algorithm terminates successfully when the zero of the merit function
has been found; this point corresponds to the zero of the normal map,
as well as to a solution of the MCP.

Credits
-------
The [MAATLAB program](https://raw.github.com/haraldschilly/compass-solver-matlab)
was originally written by Stefan Schmelzer (University of Vienna) as part
of his [diploma thesis](http://www.mat.univie.ac.at/~neum/software/compass/COMPASS.html).
Please inform the author at schmelzer-AT-ihs.ac.at if you make serious use of this code.
