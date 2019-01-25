# What are the key strengths/contributions of this paper?

This paper by Clark very clearly presents the justifications for key design decisions in the construction of the internet. Before reading this, much of the seven layers of the internet seemed arbitrary when in reality, much of the design was motivated by simple principles.

Key principles in the internet: 1) multiplexed utilization of the existing interconnected networks, 2) reliability under failure, 3) support for multiple classes of services (e.g. voice vs TTY) and 4) support for several types of networks (e.g. radio or ARPANET).

The key contribution of this work is to clearly present the motivations for fundamental designs that may have been lost along the design process. The datagram protocol was chosen to simplify fault-tolerance, to enable stateless and best-effort switching and finally to enable diverse network implementations through minimal assumptions on the link layer.

# What, if any, would you say are the weaknesses of this paper?

I enjoyed this paper. Some of it's insights I feel could not necessarily be part of the original design process and are instead from hindsight. The paper underlines a basic tradeoff in systems: fault-tolerance vs latency vs throughput. I feel some of this understanding about these tradeoffs with regard to fault-tolerance are modern post-internet insights. Another weakness of the paper is that some portions are artifacts of its time. We see how the paper recounts major design decisions in the light of the research problems of the late 80s (e.g. accountability which we still arguably don't have).

# Would you say this is an important paper? Why?
This paper is a good paper and important for a simple reason: often, the true motivations for large system design are not communicated clearly. For such an important piece of infrastructure like the internet, such design decisions are important to recount.

# Did you enjoy reading this paper?
I enjoyed reading this paper. The key ideas also generalize to interesting areas elsewhere in systems. I am working on a project on GPU multitenancy and tradeoffs described in the paper seem to hold up outside its key field.
