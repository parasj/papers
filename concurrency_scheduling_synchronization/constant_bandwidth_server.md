# Constant Bandwidth Server: Integrating Multimedia Applications in Hard Real-Time Systems
[Paper link](https://drive.google.com/open?id=19Zk7tykkZsDBCY5izwLgJ9fiIkZfhatB)

This is an example of a server implements soft real-time guarantees. With high probability, it attempts to meet deadlines. It demotes tasks that overrun a set time budget in order to limit the impact of that task on the rest of the system, allowing it to retain good performance for soft real-time tasks.

Abeni and Buttazzo present an OS scheduler that, at its core, balances between serving tasks with some mean time bound $$\mu$$ while still servicing tasks with hard deadlines $$(C_i, T_i)$$. They construct the problem as a minimization problem which then allows them to split the scheduler into two parts: hard scheduler (handled by the EDF algorithm) and the soft scheduler (handled by a new CBS scheduler).

Effectively, the CBS scheduler sounds much like the credit scheduler in Xen where there is a total budget and each task eats into that budget until it is depleted. However, it is interesting as it each dask doesn't get a anti-starvation boost. The goal for CBS is to ensure isolation. The paper presents simulation results and some empirical results. However, my main criticism of the paper is that it spent a lot of time and effort to prove that the system preserved isolation, yet the analysis did not clearly demonstrate that was guaranteed in the solution.

My main question is how this approach will scale to multi-core systems. It does neatly address this issue in the context of single core machines, but even in 1998, there were SMP systems.
