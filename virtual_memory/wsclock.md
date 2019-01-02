# WSClock - a simple and effective algorithm for virtual memory management
Key ideas:
* Working sets are a good way to reduce memory use but is expensive.
* The clock algorithm (FIFO) is simple to implement but may suffer issues like thrashing (due to global competition) and hard-to-tune parameters.
  * Not sure how big a deal adaptive parameters are, ARC shows that this is desirable sometimes and can be managed with simple policies
* WSClock is a mash-up of the two algorithms that is efficient (cheap) to implement but also has the good accuracy from working set

Outline:
* Local vs global policies
  * Local = estimate needs of a single process and allocate to satisfy each individual
  * Global = estimate without making explicit measure of per-process needs
* Interactive systems require far more allocated memory than may be available. Lots of different tasks that may be running for long time spans.
* Local algorithm is working set policy. Determining the actual working set is expensive and high overhead
* Global algorithm is clock algorithm (FIFO) where pages are arranged in a ring with a pointer moving around it.
  * Clock stores extra information per page which WSClock claims is important to minimize given the huge virtual memory spaces of modern computers.
* As WS is estimated from resident set, memory can be overcomitted (I don't 100% understand this though). So they introduce a limit on the number of concurrently loading tasks.

I glossed over the algorithm specifically, but detailed notes are available at http://pages.cs.wisc.edu/~thanhdo/qual-notes/mm/mm0-ws.txt.