---
title: Garbage Collection in Java🗑️
date: "2021-01-06 T22:12:03.284Z"
description: "Automatic Garbage Collection in Java"
---

Java Provides Automatic Garbage collection that is it allocates and deallocates memory by itself so that it eliminates the overhead on programs to do this task. The process of garbage collection is said to have basic processes:
**marking**: here all the referenced and live objects are marked in the memory by the garbage collector.
![Marking](./Marking-gc.png)

**normal deletion**: after marking, the unreferenced or the memory spaces that are not in use is deleted. The memory allocator then holds the references to the resulting free spaces.
![Marking](./Deletion-gc.png)
