# Redis Distributed Lock
This is an exercise I thought of to learn more about in-memory [distributed locking](https://www.hellointerview.com/learn/system-design/in-a-hurry/key-technologies#distributed-lock).  It is applicable to problems like [Design Ticketmaster](https://www.hellointerview.com/learn/system-design/answer-keys/ticketmaster#1-how-do-we-improve-the-booking-experience-by-reserving-tickets) where we want to hold "inventory" until a user has a chance to complete the checkout.  It also can be used in [ride sharing driver matching](https://www.hellointerview.com/learn/system-design/answer-keys/uber#3-how-do-we-prevent-multiple-ride-requests-from-being-sent-to-the-same-driver-simultaneously) where we want to only give a driver one ride request at a time.

## Resources
- [Redis lock](https://redis.io/glossary/redis-lock/)
- [Locks with timeouts](https://redis.io/ebook/part-2-core-concepts/chapter-6-application-components-in-redis/6-2-distributed-locking/6-2-5-locks-with-timeouts/)

## Approach
Implement a multi-threaded simulation of a locking algorithm.  Model trying to acquire a lock and hold it.  Report on statistics like:
1. number of attempts to acquire
2. median and p90 time to acquire per attempt
3. verify lock is still held at n-1 seconds
4. verify lock is not held at n+1 seconds

## Implementation Ideas
Start off with each thread writing to `stdout` and redirect output to a file as CSV.  Then read the output CSV with [duckdb.](https://duckdb.org/)
After the locking portion works and I would like to optimize the analytics, look into message passing back to the main thread and write out a native columnar file from the main thread.