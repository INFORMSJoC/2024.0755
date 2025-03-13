[![INFORMS Journal on Computing Logo](https://INFORMSJoC.github.io/logos/INFORMS_Journal_on_Computing_Header.jpg)](https://pubsonline.informs.org/journal/ijoc)

# Spatial branch-and-bound for nonconvex separable piecewise linear optimization

This archive is distributed in association with the [INFORMS Journal on
Computing](https://pubsonline.informs.org/journal/ijoc) under the [MIT License](LICENSE).

The software and data in this repository are a snapshot of the software and data
that were used in the research reported on in the paper 
[Spatial branch-and-bound for nonconvex separable piecewise linear optimization](https://doi.org/10.1287/ijoc.2024.0755) by Thomas Hübner, Akshay Gupte and Steffen Rebennack. 


## Cite

To cite the contents of this repository, please cite both the paper and this repo, using their respective DOIs.

https://doi.org/10.1287/ijoc.2024.0755

https://doi.org/10.1287/ijoc.2024.0755.cd

Below is the BibTex for citing this snapshot of the repository.

```
@misc{Huebner_Spatial_2025,
  author =        {Thomas H{\"u}bner, Akshay Gupte, Steffen Rebennack},
  publisher =     {INFORMS Journal on Computing},
  title =         {{Spatial branch-and-bound for nonconvex separable piecewise linear optimization}},
  year =          {2025},
  doi =           {10.1287/ijoc.2024.0755.cd},
  url =           {https://github.com/INFORMSJoC/2024.0755},
  note =          {Available for download at https://github.com/INFORMSJoC/2024.0755},
}  
```

## Description

This repository contains the code used to conduct the computational experiments described in the paper *Spatial branch-and-bound for nonconvex separable piecewise-linear optimization*.

In our experiments, we generated random instances of network flow and knapsack problems with piecewise-linear functions (PLFs) in the objective. The code to generate those random instances can be found in *instance_generation.py*. 

We compare the following methods to solve those random instances:
 - our **sBB algorithm** implemented in *sBB_main.py*, which uses auxiliary functions from *sBB_functions.py*.
 - **Gurobi's** built-in **MINLP** and **PLF-MILP solver** implemented in *gurobi_solver.py*.
 - **logarithmic MILP models** solved by Gurobi and generated via the toolbox [PiecewiseLinearOpt.jl](https://github.com/jump-dev/PiecewiseLinearOpt.jl) (implemented in *MIP_solver.jl* in *Julia-MIP*).

The sBB algorithm is implemented in Python, and the Gurobi built-in solvers are executed via the Gurobi Python API. On the other hand, the logarithmic MILP models are generated in Julia via JuMP and solved by Gurobi. The reason why we split the code is to make use of the above-mentioned toolbox for logarithmic PLF models.

## Replication

To replicate our experiments, proceed as follows:
- **Experiment I:** Network flow problems with continuous concave PLFs (Table 1). Run code in *main.py* and set parameter "problem" to "network flow". Then, run code *main.jl* in *Julia-MIP* with the parameter "problem" set to "network flow" to solve the same random instances with the logarithmic MILP models in Julia. After running the code, the results are saved as CSV files in *Julia-MIP/results*, detailing the computation times for different methods. Additionally, another set of CSV files in *Julia-MIP* contains both computation times and problem parameters. To understand the format of these results, refer to *main.py*. 
- **Experiment II:** Knapsack problems with continuous non-concave PLFs (Table 3).  Run code in *main.py* and set parameter "problem" to "knapsack". Then, run code *main.jl* in *Julia-MIP* with the parameter "problem" set to "knapsack" to solve the same random instances with the logarithmic MILP models in Julia. After running the code, the results are saved as CSV files in *Julia-MIP/results*, detailing the computation times for different methods. Additionally, another set of CSV files in *Julia-MIP* contains both computation times and problem parameters. To understand the format of these results, refer to *main.py*. 
- **Experiment III:** Knapsack problems with continuous concave PLFs (Table 5). Run code in *main.py* and set parameter "problem" to "concave-knapsack". Then, run code *main.jl* in *Julia-MIP* with the parameter "problem" set to "concave-knapsack" to solve the same random instances with the logarithmic MILP models in Julia. After running the code, the results are saved as CSV files in *Julia-MIP/results*, detailing the computation times for different methods. Additionally, another set of CSV files in *Julia-MIP* contains both computation times and problem parameters. To understand the format of these results, refer to *main.py*. 
- **Experiment IV:** Network flow problems with discontinuous l.s.c. PLFs (Table 7). Run code in *main.py* and set parameter "problem" to "discontinuous network flow". After running the code, the results can be found as CSV files in *Julia-MIP* containing both computation times and problem parameters. To understand the format of these results, refer to *main.py*.
- **Experiment V:** Knapsack problems with smooth nonlinear functions approximated by PLFs (Comparison with global solvers, Table 8). Run code in *main.py* and set parameter "problem" to "global-knapsack". After running the code, the results can be found as CSV files in *Julia-MIP* containing both computation times and problem parameters. To understand the format of these results, refer to *main.py*.
- **Experiment VI:** Improvement of solution quality by refinement of PLF approximation (Table 4). Run code in *main_approximation.py*. After running the code, the results can be found as CSV files in the same directory. To understand the format of these results, refer to *main_approximation.py*.

Executing *main.py* and *main.jl* as described above triggers the following process: After generating random instances with *instance_generation.py*, the sBB algorithm (*sBB_main.py*) and Gurobi solvers (*gurobi_solver.py*) solve them. Instance details (PLF breakpoints, problem parameters) and computation times are saved to a CSV. When running *main.jl*, the problem is reconstructed from the CSV, converted to a logarithmic MILP, and solved with Gurobi (*MIP_solver.jl*).

*Note:* Python, Julia and Gurobi Optimizer are needed to replicate our experiments. 




