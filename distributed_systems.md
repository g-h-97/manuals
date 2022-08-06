

# Introduction

Why using distributed systems is a requirement in todays world

- High Performance
- Scalability
- Security
- Availability
- Parallelism

# Infrastructure

What kind of systems we can distribute

- Storage
- Communications
- Computations

# Abstraction

Ideally, we want to talk to distributed systems as if they are none-distributed by using high level abstractions to interface with these systems, however, it seems that this is a difficult goal to achieve.

Abstraction is achieved using programming techniques such as:

- RPC
- Threads
- Concurrency Control


# Fault Tolerance

- Consistency
Is a propriety of a distributed system, and it represents the level of certainty the distributed system that the read data is correct. It can be `Stronge` or `Weak` depending on the distributed system, in the first case the correctness of the read data is guarantied where in the second not really.

- Availability
In case of *limited* number of failures, a distributed system can guarantee that it will or will not be available for operations.

- Recoverability
A distributed system can assert that in case of fault it will be eventually available, this property is a special case of *Availability* 

- Non-Volatile Storage
Allowing the dist system to save state to persistent storage is key element to a fault tolerant system.

- Different Failure Probability
By making the probabilities of failure between distributed system's element extremely different amongst each other, we can "guarantee" that our dist system is Fault Tolerant.

# Issues

- Crash
A process crashes before termination

- Byzantine Failures
A malicious or misbehaving process(es) exists on the systems, providing wrong informations

- Send Failures (Send Mission Failures)
A process crashes before sending

- Receive Failures ( Receive Mission Failures)

## Consensus Problem

- Agreement
Different correct processes must take the same decision

- Validity
If a process decides a correct, that value must be an initial value of one of the processes. Since the set out of which the decision has been made must contain all initial values of all processes.
Say for example to decide the maximum value, where every process will generate a random value v, shares it's v value with all other processes then compute the maximum value on the set V, at the end of the final round of execution the max(V) must be one of the initial values that the processes generated at the start.

- Termination
All processes must decide eventually

## Uniform Consensus Problem

- Uniform Agreement
- Uniform Validity
- Termination

## Early Decision Consensus (Solution for Crashes)

f = number of crashes
t = maximum allowed number of crashes

If `f <= t` it fine, for correct execution the distributed system must run for `r=f+1` round in total, in worst case scenario it will run for `r=t+1` rounds.

In case of no failures `r=0+1` meaning the execution end in `r=1` rounds

## Early Decision Uniform Consensus (Solution for Crashes)

`r=f+2`

# Example of Distributed System

## Google MapReduce Framework

One of earliest and simplest distributed systems on earth, made by Google mainly to go through internet indexes and rank pages depending on their importance. It became today one of the simplest dist systems to use.

It consists of:
- Master server
- Worker servers

The master distributes the work amongst the workers, it also makes sure that each worker is going to process the data on it's local disk so that workers avoid large file transfers over the network which is orders of magnitude slower than any other operation.

- GFS: Google File System
Makes sure that the data is distributed amongst the workers in 64KB chunks

- Map Function


- Reduce Function

# Proprieties

- Univalent
In a binary consensus system, a univalent system is a system where the final decision has already been made (1 or 0) but the nodes must continue the execution to reach that decision. When the final decision of a system is 0 the system is called `zero-valent` or `0-valent`, on the other hand if 1 it's called `one-valent` or `1-valent`

- Bivalent
A proof: we assume that a process with value 1 crashed before sending in a univalent configuration, depending on that system this may be the difference between that system being zero-valent or one-valent. Hence this system is Bivalent.
