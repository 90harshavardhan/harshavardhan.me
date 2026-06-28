---
title: Distributed Cache and Consistent Hashing
author: Harsha Vardhan
date: 2018-10-22T05:36:15+00:00
draft: true
categories:
  - system-design-architecture
  - system-performance-scalability
tags:
  - consistent hashing
  - distributed cache
  - hardware locale

---
A _**distributed cache**_ is an extension of the traditional concept of cache used in a single _**locale**_.  
In computer architecture a _**locale**_ is an abstraction of the concept of a localized set of hardware resources which are close enough to enjoy uniform memory access. For instance, on a computer cluster each node may be considered a locale given that there is one instance of the operating system and uniform access to memory for processes running on that node.

**_Consistent hashing_** is a special kind of hashing such that when a hash table is resized, only K / n keys need to be remapped on average, where K is the number of keys, and n is the number of slots. In contrast, in most traditional hash tables, a change in the number of array slots causes nearly all keys to be remapped because the mapping between the keys and the slots is defined by a modular operation.