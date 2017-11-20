---
layout: post
title: Riak 2.1.3 Resource Friendly Release
author: Ali Riza Keles
---

Basho announced two new minor releases of Riak KV a few months ago. As expected, these minor releases doesn't have many new features, but many bugfixes and improvements on performance issues finally some configuration changes, etc.

Before rebuilding our Riak clusters, we did some benchmarks and tests. In this post, I want to share benchmark results, which are really impressive especially on consumption of cpu and ram resources.

Physical Environment:

Test cluster was composed of 5 node Virtual Machines on a private OpenStack Installation.
Each VM has 4 vcpu and 8 GB of Ram running Ubuntu version 14.04.03.
We've used prebuilt Riak deb packages for Ubuntu.

Configuration

Let me explain a little bit configuration of Riak. We have set Riak "multibackend" backend mode and default backend is Bitcask. Search is on and that means notable cost of ram and cpu usage because of java and solr. Also strong consistency is on.

Lastly, we've used Basho's benchmark tool compiling it from source code and generated data for riak only one node. It means that this is not a capacity test and not realistic enough to see the limits of Riak. Our purpose to see improvements by comparing previous tests.

We did both short and long running tests. Short tests were only 8 minutes and the long running ones were about 32 minutes. For each type of test we did two different tests increasing concurrency: 500 and 1000 concurrent connections.

So the results are as follows:

500 Concurrent 8 Min500 Concurrent 32 Min1000 Concurrent 8 Min1000 Concurrent 32 Min

Especially when checking with long running tests it is so easy to see performance and stability of Riak KV cluster. First of all it is remarkable to have only ~250 errors since the average of operation per second was approximetly 4500. During 32 minutes, with 1000 active concurrent connections this result is great. We got ~3400 ops/sec for older Riak v2.1. with same suit.

At the beginning of tests, ram usage of each machine was around ~900MB. And after 32 minutes it was around ~1500MB. Also total average of CPU usage was %75. These numbers shows that resource consumption are more controlled and successfully managed with this version.

Riak is now more resource friendly o/

We will continue to publish Riak specific articles soon.
Stay tuned!
