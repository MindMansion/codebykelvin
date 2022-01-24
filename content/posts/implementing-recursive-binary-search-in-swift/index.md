---
title: "Understanding and implementing recursive binary search in swift"
date: 2021-12-14T21:57:40+08:00
lastmod: 2022-01-01T16:45:40+08:00
draft: false
author: "Kelvin"
description: "How to Implement a recursive binary search algorithm in Swift."
resources:
- name: "featured-image"
  src: "recursive-binary-search.png"
tags: ["Swift", "Algorithms"]
categories: ["Articles"]

lightgallery: true

---

<!--more-->

Recursion is one very interesting subject in computer science. It is so interesting that the more you read about it,
the more intrigued you become, and would like to learn more about the concept behind it.

## What is recursion in computer science?

Recursion is a concept of calling a `function` or `method` within itself *(`without a loop`)* over and over again until
a certain condition is met, and that condition is called the `kill switch` or `base case`.

### The kill switch

The **kill switch** is very important in a recursive function just like how a switch is important for a light
bulb because without a switch the light bulb will continue to light until it eventually dies, and without
a `kill switch` for a recursive function it will run into an infinity loop and continues until your
computer memory gets overflowed, and you wouldn't want that.


### Recursive function example

The example below is a simple recursive function that accepts a value `n` then calculates and return
the `factorial` of that value `n` using the factorial formula:

> **Recursive formula**
$$n! = n\sdot(n - 1)! \\ when \enspace n \eqslantgtr 1$$


```swift
func factorial(of n: Int) -> Int {
    if n <= 1 {
        return 1
    } else {
        return n * factorial(of: n - 1)
    }
}
```

#### Kill switch

{{< admonition example "Kill Switch/Base case" >}}
``` swift
if n <= 1 {
    return 1
}
```
{{< /admonition >}}


The `n <= 1` is our kill Switch, the factorial of both `1 and 0` is `1`  and there is no reason to call the
function body again. If we didn't implement the kill switch the function will keep calling itself forever
even when `n` is no longer positive and this already defies the formula rule which states that `n` must
be greater than 1.

## Recursive binary search

In this example, I will show you how to implement a binary search function using the recursion method
(there will be no loops involved).

{{< admonition warning "Binary search" >}}
Before We proceed if you don't understand how binary algorithm works I suggest you take a look at the previous post on
binary search [`here`](/posts/implementing-binary-search-in-swift)
{{< /admonition >}}

### 1. Create function

```swift
func recursiveBinarySearch(for value: Int, in items: [Int], left: Int, right: Int) -> Int? {
    var mid = (left + right) / 2
}
```

What we have just done above is pass the variables that will be used to calculate the `middle` of array to the function
itself since we no longer have a loop to help us update their values each time, just like [`usual`](/posts/implementing-binary-search-in-swift).

### 2. Add a kill switch
Now let's add a kill switch so that our function will know when to _**stop**_ looking for value i.e. calling itself.

``` swift
func recursiveBinarySearch(for value: Int, in items: [Int], left: Int, right: Int) -> Int? {
    var mid = (left + right) / 2

    if left > right {
        return nil
    }
}
```

Our kill switch states that whenever the `left` is bigger than the `Right` it should stop looking for value and
just return `nil` because our `value` was not found.

### 3. Return found value
The second kill switch, the `else if items[mid] == value` this will make sure that the function stops calling
itself again when our value is found and return it.

```swift
func recursiveBinarySearch(for value: Int, in items: [Int], left: Int, right: Int) -> Int? {
    var mid = (left + right) / 2

    if left > right {
        return nil
    } else if items[mid] == value {
        return mid
    }
}
```

### 4. Recursive call
Now let us add the complete body in charge of calling the functions for updating
`left` and `right` for recalculation of `middle`

```swift
func recursiveBinarySearch(for value: Int, in items: [Int], left: Int, right: Int) -> Int? {
    var mid = (left + right) / 2

    if left > right {
        return nil
    } else if items[mid] == value {
        return mid
    } else if items[mid] < value {
        return recursiveBinarySearch(for: value, in: items, left: mid + 1, right: right)
    } else {
        return recursiveBinarySearch(for: value, in: items, left: left, right: mid - 1)
    }
}
```

### Testing the binary search function

```swift
let numbers = [-2, 0, 1, 4, 10, 20, 30, 40, 50, 60, 70, 90]
let value = 30

if let index = recursiveBinarySearch(for: value, in: numbers, left: 0, right: numbers.count - 1) {
    print("Index is : \(index) for value: \(numbers[index])")
}

let valueTwo = -50

if let index = recursiveBinarySearch(for: valueTwo, in: numbers, left: 0, right: numbers.count - 1) {
    print("Index is : \(index) for value: \(numbers[index])")
} else {
    print("value: \(valueTwo) is not in numbers")
}
```

## Conclusion

This marks the end of this tutorial on recursive binary search algorithm implementation in swift.
Hope you had fun reading along, report any typos, or errors, and I will follow up.