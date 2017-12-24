---
layout: post
title: Divergent
published: true
---

Nope, not about an angst-ridden teenage girl trapped in a dystopia ‒ the title just refers to occasionally diverging from conventional wisdom when writing software, because Your Mileage May Vary, a LOT.

This post was inspired by some recent events that occurred when I was working on [A1icia](https://github.com/markhull/A1icia "A1icia GitHub link"), specifically [A1icia Foxtrot](https://github.com/markhull/A1icia/tree/master/A1icia%20Foxtrot/src/com/hulles/a1icia/foxtrot "A1icia Foxtrot GitHub link"). Foxtrot is the A1icia module that performs "introspection" ‒ it analyzes various metrics for the environment in which A1icia is running. For example, Foxtrot reports on file system usage, CPU temperature, database connectivity, and things of that nature.

I was writing some code to check what IP addresses are in use on the host machine, and I decided to test out [networktools by Gerald-M](https://github.com/Gerald-M/networktools "networktools link"); they were written in Java, a *sine qua non*, and the project looked like it might work well when adapted to my needs and idiosyncrasies.

I was adapting away to create a test version of LanScan that I could try out, and I came across this code in LanScan.java:

```java
private final ExecutorService scanExecutor = Executors.newFixedThreadPool(1000);
```

"Hmmm," I said to myself. "The poor naïve author doesn't realize that having an Executor fixed thread pool of 1000 will just hinder the efficiency of the program, not enhance it. Everyone knows that the optimum number of threads to use is roughly the number of cores of the machine it runs on, plus one or two more. More than that and the program will expend too many resources just creating and destroying threads instead of running at warp speed like we want." 

I knew this because I use Java Executors a lot in A1icia; her fundamental Guava asynchronous busses, for example, are built using Executors. Because of this, I had looked up and read various articles and white papers relating to this topic on the Internet (google "java executor optimum number of threads" or something like that to try it yourself), and **all** of the articles concluded that some rule resembling the one I stated above ‒ "number of cores + 1 or 2" ‒ probably would yield the optimal results. I should mention here that the more responsible authors also covered their asses by saying that you should benchmark your code yourself, because YMMV.

Prior to experimenting with **networktools** I had run a bunch of other tests using various algorithms and adapted programs to detect which LAN addresses were in use on a given machine, and because the number of possible addresses is large (10200 IP addresses at that point) and each attempt waited 2.5 seconds for a response, the trials took a long time to run. Of course, running the trials serially would take (2.5 seconds X 10200 addresses = 25500 seconds, or) c. 7 hours, which seemed a bit excessive to wait for a real-time response, so I had used thread pools in my own attempts and gotten it down to about 20 minutes, **yay**. Although sitting and waiting 20 minutes for a response from A1icia probably wouldn't appeal to most users, so **not yay**.

(start tl;dr)
If you're curious, I was using an 8-core processor running the Eclipse JVM, scanning two subnets of 5100 IP addresses, of which 7 addresses were reachable. I used a 2500ms timeout for the ping attempt, ergo there was a hard bottom limit for the run of 2.5 seconds if *any* of the addresses was unreachable.
(end tl;dr)

And because I wanted **yay** I kept trying out different things; I'm stubborn about things like that. That's when I got to LanScan. I knew it would suck wind because of the thread count but I tried it out anyway. Holy shit! Bam! About 15 seconds for the entire run. I figured there was something wrong with the code so I took it apart and audited it and benchmarked it; sure enough, it hit every address and worked great in 15 seconds. I conducted more rigorous trials and here are my benchmark results:

|**#threads**|**seconds**|
|----------------|:-------------:|
| 4 | 3185.9 |
| 8 | 1595 |
| 10 | 1276.1 |
| 16 | 798.2 |
| 50 | 255.2 |
| 100 | 127.6 |
| 500 | 27.5 |
| 1000 | 15 |
| 5000 | 5 |

Interesting, no? I found out that the optimal numbers of threads in a fixed thread pool for this case was around 8000!  I also ran trials on a caching thread pool, which I otherwise would not have tried for this use case, and it ran even slightly faster than the fixed-8000 run, so I used that.

I suppose the morals of this story must be **a)** be careful of who you call naïve; **b)** don't believe everything you read; and **c)** benchmark that problematic code, because **Your Mileage May Vary**. Also, a big shout out to the author of networktools, who reminded me of these lessons. Thanks for the useful and informative code.

- Hulles





