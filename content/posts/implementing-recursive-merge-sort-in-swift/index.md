---
title: "Implementing recursive merge sort in swift"
date: 2021-12-10T21:57:40+08:00
lastmod: 2022-01-10T16:45:40+08:00
draft: false
author: "Kelvin"
description: "Understanding and Implementing the merge sort algorithm recursively in Swift."
resources:
- name: "featured-image"
  src: "merge-sort-img.png"

tags: ["Swift", "Algorithms"]
categories: ["Articles"]

lightgallery: true

---

<!--more-->

## What is a Mergesort algorithm?

The **mergesort** algorithm is one of the popular and efficient divide and
conquer algorithms in computer science, and it is used for sorting a list of items.

While there are a few different **mergesort** algorithm functions, I will be discussing
the `top-down method` in this article.

### How it works

Mergesort is a sorting algorithm that uses a divide and conquer method to sort a list, by recursively
dividing the list into two equal sizes commonly named `left` and `right` and it continues
to `(apply the same logic)` each side of the division until only one item is remaining.
After the divisions it will then proceed to sort and merge each of the sides back together again.

#### Example
In this example I will be showing you how to implement a merge sort algorithm in Swift,
we will be using the merge sort to sort a list of random numbers.


{{< admonition note >}}
From the illustration above and explanation of the algorithm, we can see that we have
three important aspect of the merge sort, the `splitting process`, `sorting process`,
and the `merging process`
{{< /admonition >}}

### MergeSort

We are going to build and separate these machines (functions) away from each
so that we can focus directly on what each machine needs to accomplish and build it.

#### 1. Splitting process function

This function will be in charge of splitting the items and returning a sorted
version of the items.

```swift
func mergeSort(for items: [Int]) -> [Int] {
  var leftItems:[Int]
  var rightItems: [Int]
  var result: [Int]

  let length = items.count
}
```

##### State variables
Below are the explanation to the new variable we have just introduced in the function.

- **leftItems**: We are using it to store the state of each left item of a division
- **rightItems**: We are also using it to store the state of each right division
- **result**: Use for storing the result of each  `sort and merge operation`
- **length**: Used for tracking the size of each side of the division


```swift
func mergeSort(for items: [Int]) -> [Int] {
  var leftItems:[Int]
  var rightItems: [Int]
  var result: [Int]

  let length = items.count
  
  if length <= 1 {
      result = items
  }
}
```

##### Base case

{{< admonition example >}}
```swift
if length <= 1 {
    result = items
}
```
{{< /admonition >}}

checks if the size of items (the list) `is less than or equal to 1` return from the function
and quit further splitting. Obviously there would be nothing else to split at
this point.

```swift
func mergeSort(for items: [Int]) -> [Int] {
  var leftItems:[Int]
  var rightItems: [Int]
  var result: [Int]

  let length = items.count
  
  if length <= 1 {
      result = items
  } else {
      leftItems = Array(items[0..<length / 2])
      rightItems =  Array(items[(length / 2)..<length])
      
      result = merge(for: mergeSort(on: leftItems), and: mergeSort(on: rightItems))
    }
    return result
}
```

##### Splitting the items list

We added an else statement, this will be in charge of splitting the list
whenever the `(size)` length is greater than `1`

- `leftItems` and `rightItems`: Here we are initializing the leftItems to contain an
  `Array` of half size of the items list whenever the function calls itself.
- `result`: The result, is initialized with result of calling the `merge` function
  that is in charge of sorting and merging each division of the items list.
  Though the `merge` function, is not yet implemented, and we will do that next.


{{< admonition tip >}}
Note that here we used the Swift Array subscript syntax to divide each
list items and grab the half of it, instead of using a loop to iterate over
the entire list items to grab the half of it.  
i.e. items`[0..< n/2]` will produce half of the items
{{< /admonition >}}


#### 2. The merge function

This function accepts and two different lists `leftItems` and `rightItems` which are
the left and right sides of items list division. The function will now compute
and return the result of sorting and merging each list items.

```swift
func merge(for leftItems: [Int], and rightItems: [Int]) -> [Int] {
  var result = [Int]()
  var rightPosition = 0
  var leftPosition = 0
}
```

- `result:` This will be used to store the result of sorting each item.
- `rightPosition and leftPosition:` This is used to track the index of each list item starting from `0`

```swift
func merge(for leftItems: [Int], and rightItems: [Int]) -> [Int] {
  var result = [Int]()
  var rightPosition = 0
  var leftPosition = 0
  
  while (leftPosition < leftItems.count || rightPosition < rightItems.count) {
    // more to come
  }
}
```

Here we are checking for when either of the list size is greater than either of `positions`  index.
It makes sense to only do something whenever we have items with size  `greater` than `1`

##### Sorting and merging

```swift {7-12} showLineNumbers
func merge(for leftItems: [Int], and rightItems: [Int]) -> [Int] {
  var result = [Int]()
  var rightPosition = 0
  var leftPosition = 0
  
  while (leftPosition < leftItems.count || rightPosition < rightItems.count) {
    if (leftPosition < leftItems.count && (rightPosition >= rightItems.count || 
        leftItems[leftPosition] <= rightItems[rightPosition])) {
      
      result.append(leftItems[leftPosition])
      leftPosition += 1
    }
  }
}
```

##### Copying from leftItems

Here we are copying from leftItems list only when the value in the leftItems list is
smaller than the value in rightItems list `(rightPosition >= rightItems.count || leftItems[leftPosition] <= rightItems[rightPosition])`
or when there are no items left in the rightItems. We then add increase the value of `lefPosition` by `1` after.

```swift
func merge(for leftItems: [Int], and rightItems: [Int]) -> [Int] {
  var result = [Int]()
  var rightPosition = 0
  var leftPosition = 0
  
  while (leftPosition < leftItems.count || rightPosition < rightItems.count) {
    if(leftPosition < leftItems.count && (rightPosition >= rightItems.count ||
     leftItems[leftPosition] <= rightItems[rightPosition])){
        
        result.append(leftItems[leftPosition])
        leftPosition += 1
    } else {
        result.append(rightItems[rightPosition])
        rightPosition += 1
    }
  }
  return result
}
```

##### Copying from rightItems

Here we are copying from the right items whenever the if statement conditions fails.

## Testing the function

```swift
var myList = [10, 5, 13, 12, 18, 38]
let sortedList = mergeSort(on: myList)

print(sortedList)
```
Output: `[5, 10, 12, 13, 18, 38]`
