Part 4 Collections
====================================
Learning objectives

### 4.1. Collections overview
After completing this lesson, you should be able to:
* Understand the structure of the Scala Collections hierarchy 
* Describe how to apply functions to data in collections 
* Outline the basics of structural sharing
* Illustrate the performance characteristics of different data structures

### 4.2. Sequences and Sets
After completing this lesson, you should be able to:
* Describe the various kinds of sequence collections and their properties
* Outline the desirable properties of the Vector collection type
* Describe the properties of set collections

### 4.3. Options
After completing this lesson, you should be able to:
* Describe the relevance of Option in the Scala type system
* Outline how to use Option in your types

### 4.### 4. Tuples and Maps
After completing this lesson, you should be able to:
* Describe what a tuple is and how they are used
* Outline how to deconstruct tuples
* Describe the properties of a map

### 4.5. Higher Order Functions
After completing this lesson, you should be able to:
* Describe the application of functions to data
* Outline basic usages of higher order functions in Scala

---------------------------------------------------------------------------------------------

#### Scala - Collections
 
Scala has a rich set of collection library. Collections are containers of things. Those containers can be sequenced, linear sets of items like List, Tuple, Option, Map, etc. The collections may have an arbitrary number of elements or be bounded to zero or one element (e.g., Option).

Collections may be strict or lazy. Lazy collections have elements that may not consume memory until they are accessed, like Ranges. Additionally, collections may be mutable (the contents of the reference can change) or immutable (the thing that a reference refers to is never changed). Note that immutable collections may contain mutable items.

For some problems, mutable collections work better, and for others, immutable collections work better. When in doubt, it is better to start with an immutable collection and change it later if you need mutable ones.

This chapter throws light on the most commonly used collection types and most frequently used operations over those collections.

Sr.No	Collections with Description
1	
Scala Lists

Scala's List[T] is a linked list of type T.

2	
Scala Sets

A set is a collection of pairwise different elements of the same type.

3	
Scala Maps

A Map is a collection of key/value pairs. Any value can be retrieved based on its key.

4	
Scala Tuples

Unlike an array or list, a tuple can hold objects with different types.

5	
Scala Options

Option[T] provides a container for zero or one element of a given type.

6	
Scala Iterators

An iterator is not a collection, but rather a way to access the elements of a collection one by one.

