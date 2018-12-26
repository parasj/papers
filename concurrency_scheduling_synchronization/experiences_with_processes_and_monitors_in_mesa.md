# Experience with Processes and Monitors in Mesa

[https://people.eecs.berkeley.edu/~brewer/cs262/Mesa.pdf](Paper link)

Background, Monitors: Monitors are a concept from Hoare that describe procedures that have condition variables. This sounds mostly similar to the condition variables commonly used in C/Pthreads, but it sounds like this paper described a more primative version of monitors.

**Background, MESA:** Mesa is a language from PARC that was built around separating a program's interfaces from the implementation. All programs can be typechecked against the interfaces.  This sounds similar to C headers but Mesa is not an imperative language

**Problem:** Lampson et. al. were building an OS and wanted to explore safe concurrency in the OS. However, monitors have several key issues, namely how to handle nested monitor calls (`WAIT`, exceptions),  priority scheduling for threads, I/O.

**Concurrency model in MESA:** The authors describe a typical fork-join concurrency model, and describe their justification for using monitors over cooperative scheduling (e.g. IO necessitates preemption). There follows a description of monitors in Mesa, which alone are incomplete. I like the explicit description of invariants while programming. If concurrent code today annotated such invariants, we would likely catch many more race conditions. 

* There is quite a bit of detail in the remainder of the paper, covering deadlocks, issues with monitored objects, and timeouts. I was most interested in the issue of priority inversion. It's an issue that occurs with nested locks. They propose a solution called priority boosting to address this.

* I didn't really like this paper in the end. It was very focused on Mesa which is a language with little use today. However, the issues it brings up are very relevant, some just to monitors and some to concurrency in general. I liked how it focused on enumerating the problems with monitors as many papers focus too much on the solutions.
