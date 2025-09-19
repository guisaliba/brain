a semaphore is a mechanism that can be used to constrain or control access to a shared resource access. we can make a simple mental model of with with restaurant orders:
- imagine that you went to McDonalds to order (and eat) a burger. along with you, 400 other people had the same idea at the exact same time and went to the same place to order a burger.
- what would happen if the 400 people tried to order their meal at the same time?
complete chaos is the answer for the question above. there is no sane way of allowing 400 people order their meals at the same time in a tiny place such as the McDonalds.

the employees would get crazy, people would stomp over each other, bad stuff would happen... but luckily, McDonalds operate in a fashioned way.
let's imagine the one you went to operates with 4 lines, 4 registers and 4 employees, allowing 4 orders to happen at the same time.

this means that 4 people would be ordering their meal concurrently (actually, in parallel), while the other sit and wait for their turn to place their order.

but in this case, aren't we talking about queues (specifically FIFO queues)?
yes, each line can be thought of a small queue.

but the keypoint here is what's happening at the head of all 4 lines.
people could try to order out of their turn, let friends cut, and ensue chaos.
perhaps there is a manager that sends people away if they're doing this, so the manager can be thought of an enforcing **semaphore logic**. 

suppose you have a shared resource that can be freely accessed by one or more threads. this shared resource could be a remote server, a shared in-memory datastore, a complex video transcoding pipeline.
**a system that is shared should be shared in a reliable way that doesn't allow for bombardment of the system.**

if you were trying to control access to a pipeline it would be bad if anyone could kick off 10k jobs to transcode some video, at the same time. your pipeline could crash down.

a **mutex** can be thought of a mechanism that **control multi-threaded access to code**.
it only ever allows a single thread exclusivity over this code. this is important to avoid data-races and all sorts of problems.

if a mutex is concerned with ensuring a single thread ever accesses ==_code exclusively_== ==a semaphore is concerned with ensuring== ==_at most N threads can ever access code exclusively_====.

