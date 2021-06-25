# Concurrent Datastructure Design for Software Transactional Memory

Bachelor Thesis 2021    
Vrije Universiteit Amsterdam   

## _Abstract_

This thesis investigates how transactional memory can be applied to concurrent datastructure design, specifically, how it can provide a clean and accessible interface replacing locks and built on top of lock-free primitives for concurrent algorithms. Two of such datastructures have been implemented, a transactional Red-Black Tree and a Skiplist, with underlying encounter-order and commit-time transactions taking care of concurrent insertions. Encounter-order transactions lock transactional objects as they are encountered, permitting only a single transaction modifying the object, whereas commit-time transactions lock objects only at commit-time, i.e. when the transaction tries to make its modifications atomically visible. Results show that word-based commit-time transactions, in which locks are associated with memory addresses, cannot be successfully applied to Red-Black Trees without imposing an unnatural design on the datastructure due to the fact that the commit-time transaction's write-list consists of (address, value) 2-tuples that are oblivious to the chain of dependencies between the writes. For Skiplists, no such restrictions exist, with both encounter-order and commit-time transactions exhibiting optimal scaling properties. As opposed to findings of other papers like [[1]](https://www.cs.tau.ac.il/~shanir/nir-pubs-web/Papers/TRANSACT06.pdf) [[2]](https://dcl.epfl.ch/site/_media/education/4.pdf), which promote the use of the commit-time mechanism for high-contention, this paper finds that due to a large number of aborting transactions, which are expected in case of high contention, and the more expensive commit-time API operations, the encounter-order locking mechanism outperforms commit-time locking on all metrics with a factor of two. Furthermore, it can be empirically concluded that the use of the transactional algorithm design is much less error-prone than its lock-based counterpart, without further restrictions on its structure posed by lock-free primitives. While performance-wise, hand-crafted concurrent datastructures might prove to be more effective, the transactional design can open up the process to a wider range of programmers by providing a straightforward abstraction for concurrency.

_**keywords**_: transactional memory, concurrent datastructures, parallelization
