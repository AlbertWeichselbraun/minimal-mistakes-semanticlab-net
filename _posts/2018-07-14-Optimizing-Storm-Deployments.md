--- 
title: Optimizing Apache Storm Topologies
layout: single
categories: ["Linux", "Storm", "Java"]
--- 

This article summarizes hints for optimizing and deploying Apache Storm topologies.

### Setup your storm cluster

1. I/O is zookeeper's main bottleneck - ensure that the `/data` partition of zookeeper machines serializes to quick storage (ramdisk ;)
2. Determine the number of parallelism units using the following rule of thumb:
   - *number of available CPU cores* on all machines minus one core per machine that is used for the *Acker*
   - Example: 2 machines with 48 and 1 machine with 32 cores; parallelism units = 2x(48-1) + (32-1) = 125
3. Using multiple workers per machine allows deploying multiple topologies at once (the number of workers is determined by the number of ports configured in the `supervisor.slots.ports` setting in `storm.yaml`)


### Topology configuration suggestions

1. Use one worker per machine and topology (intra-worker transports are more efficient)
2. The number of executors depends on whether your bolt is I/O or CPU bound
   - CPU bound: configure one executor per available parallelism unit
   - I/O bound: use 10-100 workers per parallelism unit, depending on the expected I/O delay
3. The total number of parallelism units in your topology should equal the number of available parallelism units


### Profiling the topology

1. Storm UI: use the capacity metric to identify bolts which require a higher parallelism
2. your `nextTuple` and `execute` methods determine the spout's/bolt's runtime - optimize these methods
3. use queue's for I/O in spouts or terminal bolts (i.e. write final results to a queue and use a writer thread that performs batch inserts to serialize the queue to disk)


### Glossary

* workers process - responsible for executing the topology on a particular machine
* executor - thread spawned by the worker for a particular component (bold or spout); the number of executors is configured by setting the `parallelism hint` parameter in the `setSpout` or `setBolt` method.
* task - number of instances of a particular bolt/spout to deploy; configuring more than one task using `setNumTasks(n)` allows to later increase the number of executors for that particular spout/bolt without redeploying the topology.



### References

 1. [Scaling Apache Storm](https://www.slideshare.net/ptgoetz/scaling-apache-storm-strata-hadoopworld-2014?qid=19b9de2b-175b-415e-94c8-7a537d8c2a9a&v=qf1&b=&from_search=2)
 2. [Understanding the Parallelism of an Apache Storm Topology](http://storm.apache.org/releases/1.2.2/Understanding-the-parallelism-of-a-Storm-topology.html)
 3. [Stack overflow - What is a "Task" in Storm Parallelism](https://stackoverflow.com/questions/17257448/what-is-the-task-in-storm-parallelism)
 4. [Hortonworks - Storm Parallelism](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.1/bk_storm-component-guide/content/storm-parallelism.html)
