Old questions: https://www2.eecs.berkeley.edu/Grads/CS/Prelims/osqu.html

# Stoica 2018

## ZY questions
Q1
* Describe paging and segmentation.  What are their disadvantages and advantages.  List a way to overcome the disadvantage.
* What's E2E argument?  Give two examples.
* Describe log-structured file system.  What are their advantages.
* What are active messages?  

Q2
* Assume you have three workloads (1) web server (2) database server (3) network file server.  You can either back these apps with (1) just SSD, (2) just HDD, (3) or a combination of the two.
* Compare SSD and HDD in several dimensions.  
* For each of these 3 workloads, discuss which storage solution you'd choose and why.
* How would your choice for 1 system change if you were to pick a parameter for a storage system and change it?

Q3
Context: Exokernel and SPIN
* What's the motivation between these classes of OSs?
* Explain the design Exokernel.
* Explain SPIN.  How is it different from Exokernel?
* Despite their academic impact they didn't take off in practice.  Discuss why.

## SK questions
1. What are the advantages and disadvantages of segmentation and paging?
2. What is the End-to-End Principle (with an example)?
3. Explain LFS. (I think there was something about active messages, but that may have just been a discussion, not sure it was an actual question)
4. What are the advantages and disadvantages of HDDs and SSDs?
5. How might you use HDDs and SSDs in some real applications?
6. If SSDs behaved differently (in a way of your choice), how would it affect the design of your applications in #5
7. Compare and contrast Exokernel and SPIN? (An extended discussion of this was the "last question" that filled the remaining time)

# Wagner Smith 2001
## Recollection #1

[Smith] Talk about viruses generally. How come PCs seem to have a lot more of them than UNIX (on UNIX you only hear about worms)? What kinds of viruses do you see? [Wagner] What changes would you make to prevent virus damage?

[Wagner] You have a system where memory chips can be unavailable for 5-6 seconds at a time; this happens about once a minute. Data isn't lost, but you get an error message on reads/writes during this period. What changes could you make to the OS to circumvent the problem? What if you had one known good chip? What if during the 5-6s period, the chip returned random data for reads and might ignore writes?

[Smith] Network-Attached Storage is a box with disks you can plug in to your Ethernet. What are the implications of doing this to increase storage vs. adding more disks to an existing box?

## Recollection #2

[Smith] Can you have viruses on UNIX? What is a virus? Why can you have viruses on Windows?

[Wagner] Right now we have smart disk controllers that reorder requests, etc. Let's say we have smart memory chips. Unfortunately, the chips are faulty -- they fail every 10 seconds and take a few minutes to reboot. What can you do about this problem? Now let's say that you get an interrupt each time a memory chip fails. What kind of support do you need for all of this? What if one of the memory chips is guaranteed not to fail? What if the chips return bad data?

[Smith] What is network-attached storage? How would you design a system for network-attached storage? The network-attached storage appears to be local disk. What are the implications of this? How fast is local disk access? How would you make network-attached storage fast? [Wagner] What are the security implications of network-attached storage?

## Recollection #3

[Smith] What is it about UNIX and PC's (did not specify the OS) that cause UNIX systems to be attacked by worms and PC by virus? What are the aspects of a worm and a virus? (which was more a helping question) What is different about PCs OS and Unix that makes one more susceptible to than another?

[The desired answer, according to Smith at the end, was that on UNIX separate data and executable into different files and Windows does not].

[Wagner] Given large intelligent memory components that have a lot of intelligence - that have the property of being on line on the order of a minute and then becoming unavailable (does not provide or receive data) for 6-10 seconds. What are the design issues with this? How would you design an OS to support this system? He allowed that there would be enough memory to have multiple copies of data in different intelligent components. As a follow up, he asked what would happen and how would you detect the situation that the components would actually start returning incorrect data rather than just not respond. Assuming you know the component if flaky how to you handle it in the OS?

[The answers range from redundant components, using parity and ECC across components, and voting for the correct answer. Also MTBF and MTTI calculations. The answer to that last question was to make the page as "non-existent"]

[Smith] Smith asked for the design issues associated with a Network Attached Storage. What are the issues if the NAS is really a full file-system instead of just a block device? The network-attached storage appears to be local disk. What are the implications of this? How fast is local disk access? What are the issues with providing high performance for NAS? [Wagner] What are the security implications of network-attached file system?

## Wagner Smith 2001
[Wagner] What would happen if the seek time of a disk increased tenfold? (Looking for: changes in disk-scheduling algorithms, LFS)

What are some problems with LFS? (complicated, not good for reads)

Random useless aside from Smith: What is the expected distance between two random cylinders? (1/3r -- Smith himself admitted this wasn't a fair question for an OS prelim, but I'm pretty sure that didn't stop him from marking me down)

What if there were a big NVRAM cache in front of the disk? (speeds up writes a lot, renders LFS useless)

What if the cache weren't NV? (loss of durability guarantees)

What if the whole disk system were 10x slower, but the CPU were 10 times faster?

Random aside from Smith: Are any systems I/O bound? Lots of research systems are (like sensor networks in smart dust), but since these were developed in the last 10 years, Smith doesn't know or care about them. No production systems are I/O bound, since they use lots of techniques to get over the I/O bottleneck.

[Smith] What assembly language instructions and registers are protected? (Looking for: setting the time, changing mode, changing registers which hold addresses of PT, interrupt handler, the actual PT, status register containing mode and other important bits)

Random aside from Smith: What is the reason that system clocks tend to run slow instead of fast? (correcting the clock ahead instead of backwards guarantees that time always monotonically increases)

How does the processor prevent user processes from executing privileged instructions? (user processes execute in user mode)

[Wagner] What infrastructure/services are there between a user and a web server? (DNS, routing)

[Smith] How do you send email transparently to a mobile computer? Hint: Smith doesn't know how DNS works, so don't try to include dynamic DNS as part of your solution. He will only get confused.

## Brewer Smith 2001
[Smith] Describe what happens on a page fault (everything)!

[Smith] What is a virtual machine? Describe what happens on a page fault in a virtual machine.

[Brewer] How is RPC different from a regular procedure call? Are there any ways to correct these differences?
