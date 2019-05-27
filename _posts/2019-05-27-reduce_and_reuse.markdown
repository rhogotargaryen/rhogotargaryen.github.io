---
layout: post
title:      "Reduce and Reuse"
date:       2019-05-27 05:11:50 +0000
permalink:  reduce_and_reuse
---


One awesome iterator method for arrays is the Reduce method.  Reduce has many practical applications ranging from score tracking to string manipulation.  The method has a lot of utility as it is able to accumulate values across an array and return that value once iteration is complete.  Let us go in depth into how the iterator works and some of its great use cases.  

The Reduce method itself like most iterators accepts a callback as its first arugment and a second argument, an *initial value*, that we will get into later.  The callback itself accepts 4 arguments though for most simple use cases he first two arguments are often the only ones used.  The first two arguments to the Reducer CB are the accumaltor and currentValue placeholders.  The first argument will be assigned the accumulator, or the value continuall being returned by the logic of our CB as we iterate through the array.  The second argument is the CurrentValue of the current element being iterated through.  Only using these two arguments the callback will run on each element of the array starting at index [1] using index[0] as the valued assigned to the accumulater, then we can use the values of the iterated elements to accumulate and return a total value.  Consider the following:

```
arr = [1, 2, 4]

arr.reduce((acc, curr) => {
  return acc + curr
})

// returns 7
```
Step by step the reduce callback begins by assigning the acc argument 1, the 0 index of the array being called on, and the curr argument a value of 2, the 1 index of the array.  The value returned by our CB on this iteration is than 3 (1 + 2). 
On the next iteration 3 will be assigned to acc, and 4 will be assigned to the curr argument.  The value 7 would be returned by our reduce method as an accumulated total of our CB's logic.



The above demonstrates the
