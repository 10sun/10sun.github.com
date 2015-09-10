---
layout : post
category : LearningNote
tags : [EffectiveC++, C++, Basis]
---
{% include JB/setup %}

**Introduction**

- *Markov chain*: a finite markov chain is a process which moves among the elements of a finite set $\omega$ in the following manner: when at $a \in \omega$, the next position is chosen according to a fixed probability distribution $P(x,.)$.
- The classical theory of Markov chains studies *fixed* chains, and the goal is to estimate the rate of convergence to stationarity of the distrubition at time *t*, as *t->infinite*.
- The modern studies is to find the asymptotics of convergence to stationary as a function of the state space size and geometry.