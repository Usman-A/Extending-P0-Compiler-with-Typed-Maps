# Adding Maps to P0

**Authors: Aleem Haq, Usman Asad, Muhammad Faisal Jaffer**

**Computer Science 4TB3**, ***McMaster University***

## Description

### Research Question
The goal of this project is to extend the P0 compiler with typed maps. The implementation of the map should be able to guarantee constant insertion, lookup and deletion time.

### Test Plan
To be able to test the efficiency of the implementation, we can measure the following operations to see if the time stays the same when size of the map linearly increases (constant time complexity)
    - Lookup from map of size 1 vs 100000000
    - Insertion in map of size 1 vs 100000000
    - Deletion from map of size 1 vs 100000000

### Documentation
We plan to use Doxygen to document our changes to the compiler and generate appropriate diagrams/PDFs.

### Insight
We hope to learn the inner workings of the P0 compiler and WebAssembly syntax. By exploring other implementations of maps in different languages (like Python and Go) we also hope to learn the design patterns used for optimizing memory.


## Resources

- [Python Grammar](https://docs.python.org/3/reference/grammar.html) - Python 3.3 grammar doc

- [Python dictionaries](https://csrgxtu.github.io/2020/04/21/Python-Dict-a-new-implementation-by-pure-Python/) - Article on Python dictionaries

- [Go Grammar](https://golang.org/ref/spec)  - Go lang spec and grammar

- [Go map](https://dave.cheney.net/tag/hashmap) - Article on Go lang map implementation

- [Cuckoo Hashing](https://cs.stanford.edu/~rishig/courses/ref/l13a.pdf) - An Overview of Cuckoo Hashing

- [Hash Tables](https://www.interviewcake.com/concept/java/hash-map) - Article on hash tables

- [Web Assembly docs](https://developer.mozilla.org/en-US/docs/WebAssembly) Mozilla developer documentation for web assembly

- [Web Assembly Syntax](https://webassembly.github.io/spec/core/syntax/instructions.html) - Web Assembly syntax and instructions document

- [Web Assembly Spec](https://www.w3.org/TR/wasm-core-1/) - Web Assembly W3c specification document

- [WASM Docs](https://github.com/WebAssembly/design) - Web Assembly Design Documents

- [Python Dictionary](https://csrgxtu.github.io/2020/04/21/Python-Dict-a-new-implementation-by-pure-Python/) - Dictionary example made in python

- [Hash maps Java](https://www.geeksforgeeks.org/internal-working-of-hashmap-java/) - Internal works of Java hash maps

- [Hash maps CPP](https://www.softwaretestinghelp.com/hash-table-cpp-programs/) - Hash maps and tables in cpp

- [Type safe hash map C](https://github.com/DavidLeeds/hashmap) - Type safe hash map implementation in C

- [Basic hash map cpp](https://github.com/aozturk/HashMap) - Basic hash map implementation in cpp


## Division of work 

| Person | Work |
| ------ | ------ |
| Aleem | Implementation, testing & presentation/docs |
| Faisal  | Implementation, testing & presentation/docs |
| Usman | Implementation, testing & presentation/docs |

## Weekly Schedule 

- Weekly meetings on Tuesdays and Saturday evenings 7pm
- Communication on discord
- Regular commits, contributions to gitlab

| Week  | Task |
| ------ | ------ |
| March 15 - 21 | Research and finalize design decisions |
| March 22 - April 4  | Implement maps to the P0 compiler |
| April 5 - 11| Test implementation |
| April 12 | Submit project artifacts |

