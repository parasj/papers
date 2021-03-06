# Lottery Scheduling: Flexible Proportional Share Resource Management
[Paper link](https://www.usenix.org/legacy/publications/library/proceedings/osdi/full_papers/waldspurger.pdf)  //  [CS162 slides](https://cs162.eecs.berkeley.edu/static/lectures/10.pdf)

**Key idea**: Probabalistic scheduling mechanism that does not have starvation and avoids priority inversion by transfering tickets. It can be extended to other resources as well.

Waldspurger and Weihl present a probabilistic mechanism for resource sharing using a lottery scheduler. The key idea behind this work is that the problem of scheduling can be modeled as a problem of randomly sampling a lottery ticket held by some task. This provides some convenient properties, namely that a task's lottery value can be adjusted to change the rate at which it is sampled. Moreover, the algorithm is simple and easy to reason about, compared to other priority schedulers. And this has the benefit of being simple to implement compared to other "microeconomic" schedulers.

The authors demonstrate that the lottery is probabilistically fair, meaning that over many allocations, a process's throughput is proportional to its number of tickets. It's quite interesting that this means that starvation is no longer an issue as any tasks has a chance of being sampled as long as it has one ticket. I enjoyed their analysis. Not related to this summary, but the authors clearly put effort into making the charts readable.

The authors implemented lottery scheduling in the Mach microkernel. The baseline for analysis was the existing Mach scheduler. I like this paper a lot. My main criticism of this work is that I don't really buy the starvation argument. This is an important point that was buried at the end of section 2. I would say that in practical systems, short-running tasks still may be rapidly crowded out by high-priority long-running tasks. So while in theory starvation is no longer an issue, in practice I think it still is.
