# Operating System

##  Scheduling

---

**Scheduling**: which process gets CPU and when

* Given multiple processes, but only one CPU
* No single best policy



FCFS: First Come First Served

* Allocate CPU to processes in order of arrival
* Non-preemptive, simple, no starvation
* Poor for short processes



RR: Round Robin

* Time-slice: each process gets quantum in turn (A->B->C-> A->B->C)
* Preemptive, simple, no starvation
* Process waits at most (n - 1) * quantum

SPN: Shortest Process Next

* Select process with shortest service time
* Optimal for non-preemptive, allows starvation
* Assumes service times are known



SRT: Shortest Remaining Time

* Select process with shortest remaining time
* Assumes service times are known
* Optimal for preemptive, but allows starvation



Multi-Level Feedback Queues

* Priority queues: 0 (high).. N(low)
* New processes enter queue 0
* select from highest priority queue k, run 2^k quantum
* Periodically boost
* Complex, adaptive, highly responsive
* Favors shorter over longer, possible starvation
* Imitate SRT without knowing service time



Priority Scheduling

* Select process with highest priority, based on external criteria (A is high, B is low)



Proportional Share

* Each process requests some CPU utilization(% of time resource is used)
* Utilization over long run, actual ≈ request
* Select process with minimum actual/request ratio (algorithm is inefficient)
* Stride Scheduling
  * For process A,B,C with requests Ra, Rb, Rc
  * Calculate ***strides***: Sa = L/Ra, Sb = L/Rb, Sc = L/Rc, where L is very large to make Sx an integer (For optimization purpose)
  * For each process x, maintain pass value Px (init 0)
  * Repeat every quantum
    * Select process x with minimum pass value Px, run
    	 Increment pass value by stride value: Px = Px + Sx	



Real Time Scheduling

* Correctness of real-time systems depend on

  * logical result of computations
  * Timing of these results

      Type of real-Time systems
      * Hard vs. soft real-time
      * Periodic vs. aperiodic
        * Periodic processes: computation is cyclic - ABABAB vs. BABABA
* Scheduling
  * Earliest Deadline First (EDF)
     * Schedule process with earliest deadline
     * If earlier deadline process appears, preempt
     * Works for periodic and aperiodic processes
     * Achieves 100% utilization (ignoring overhead)
     * Expensive: requires ordering by deadlines
  * Rate Monotonic Scheduling (RMS)	
     * Limited to periodic process. If periodic processes, prioritize based on rates (1/period)
     * Simple and efficient. Optimal for static priority algorithms. 
     * At start of period, select highest priority
     * Preempt if necessary
     * Wait till next period when burst done
     * If U1 +…	+ Un ≤ n(2^(1/n) - 1), all deadlines met (Applies only if it passes. If fails, we do not know if deadline can be met or not)
     * If sum of utilization is smaller than 69%(ln 2), the deadline is always met. (Because n(2*1/n - 1) > ln 2)

  








