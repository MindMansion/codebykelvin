---
title: "Understanding and implementing binary search in swift"
date: 2021-12-01T21:57:40+08:00
lastmod: 2022-01-01T16:45:40+08:00
draft: false
author: "Kelvin"
description: "How to Implement a binary search algorithm in Swift | a divider and conquer algorithm"
resources:
- name: "featured-image"
  src: "binary-search.png"

toc:
  auto: false

tags: ["Swift", "Algorithms"]
categories: ["Articles"]

lightgallery: true

---

<!--more-->

**Binary search** is a  `(divide and conquer)`  algorithm and one of the most popular and widely used algorithms for searching a
data structure because of its efficiency and speed.

I will be showing you how to implement a search algorithm using
the binary search method, this method of searching is what is
mostly used under the hood for **Swift** `standard library` API 
functions for searching items i.e.

- first(where: )
- last(where: )
- firstIndex(where: )
- lastIndex(where: )

## The Problem

Let's say we have an array of 12 random numbers and would like
to find `30` from this list of numbers, but you don't know which
`index` this favorite number of yours appears in the list.

{{< admonition question >}}
  To solve this problem start by asking how many times do I have to look inside this array of numbers before I
  can find my favorite number?
{{< /admonition >}}

### First Approach

Given that you know how to use loops to traverse an array and print its element, you would think to combine a `for
loop` and `if statement` on the list of numbers to find and print any index whose value is your favorite number `30`
your solution might look like the code below.

```swift
let numbers = [20, 4, -2, 0, 1, 40, 50, 60, 10, 30, 90, 70]
let myFavorite = 30

for (index, value) in numbers.enumerated() {
    if value == myFavorite {
        print("Index for favourite is: ", index)
        break
    }
}
```
Output: `Index for favorite is: 9`

#### Problem with this approach

While this might put a smile on your face knowing that you have successfully found the index of your favorite
number, and you only had to look `10 times`

But think what if this list of numbers is **_10Billion_** in length, and your favorite number is at the very end of the
list, woof! this would take 10Billion times to look inside the array of numbers, imagine if this was a person
trying to individually look inside 10Billion boxes, that would take more than a lifetime to complete but of course
computers are way faster than a human and would complete the task in a shorter amount of time compared to a
human `but` longer than it took when the list was only `12 items`.

This will make you unhappy especially when
you need your favorite number as soon as possible and don't have time to wait for this 10Billion loop to complete.

{{< admonition title="Good News!" >}}
  Good news is that a `binary search` algorithm can help reduce your wait time to a significant amount but only
  with one requirement from you.

  > The list of numbers must be `sorted` (arranged in order). Binary search can only work on a list that is sorted,
  so it is a requirement that your list of numbers must be sorted.

{{< /admonition >}}

### Binary search Approach

Start by asking yourself how many times do I have to divide **_10Billion_** by 2 until the final answer is 0?.

The solution is `34 times` which is not too many and definitely not 10Billion times.
34 times is the worst case `(The longest wait time)` for a 10Billion list of numbers the maximum time we have
to look inside the array to find our favorite number.

#### How it works

##### 1. Computed the middle index

Binary search works by first taking the total length of the array and divides it into two parts commonly known as
`left` and `right` where `left` represents the first index of the array which is `0` and `right` represents the
last index of the array which is `(n-1)` or `(numbers.count - 1)`. The outcome of this operation is called the `middle`
and it represents the middle index of the array.

```swift
let numbers = [-2, 0, 1, 4, 10, 20, 30, 40, 50, 60, 70, 90] //sorted
var left = 0
var right = numbers.count - 1
var middle = (left + right) / 2
```
##### 2. Search the array with `middle`
The next step is to take the computed value of the middle which is `5` in this case and look inside the numbers list
for our favorite number using the `middle` as the index value.

##### 3. Update the middle
If the value in the middle index corresponds to our favorite number we return it, and we are done but if not we
will check if the value in the middle index is bigger than our favorite number `(remember that our number is sorted)`
if yes then there is no need to look at any index below our current middle index, which mean we are only concerned
with the indexes above our current middle index which it to the `right` and we have just saved ourselves the huddles
of looking it `4 boxes` that are to the left.

Now that we have chosen **`NOT`** to look at the boxes below our middle index, we have to update the value of `left` because
it is no longer 0 but now `middle + 1` the reason why we are adding `1` to the middle is that we have already looked
into it, and it doesn't have our `favorite` number and there is no reason to include it again and vice versa.

```swift
let myFavourite = 30

if numbers[middle] == myFavourite {
    print("Yes Found! Your favourite number at index: \(middle) \n")
} else if numbers[middle] < myFavourite {
    print("The middle index \(middle) with value:  \(numbers[middle]) is too small")
    print("Please update left to: \(middle + 1) \n")
} else {
    print("The middle index \(middle) with value:  \(numbers[middle]) is too large")
    print("Please update right to: \(middle - 1) \n")
}
```
Output: `The middle index 5 with value: 20 is too small Please update left to: 6`

##### 4. Apply a loop
You might be thinking that now is the best time to bring it the `loop` and perform these operations, again and again,
until the favorite number index is found and yes you're correct.

Let's perform these operations inside a `loop` and update the value of the `middle` index inside the loop each time to
loop runs until the runs are completed.

The diagram below shows the steps our algorithm is going to perform until the loop life cycle is completed or
our favorite number is found.

##### Diagram

{{< mermaid >}}
  graph TD;
    A[Array] -->|Get middle| B(Value: 5)
    B --> C{"numbers[5] == 30?"}
    C -->|True| D[Return and finish]
    C -->|False| E{"numbers[5] < 30?"}
    E -->|True| F(Update left to 6)
    F --> G[Repeat the process]
{{< /mermaid >}}


```swift
let numbers = [-2, 0, 1, 4, 10, 20, 30, 40, 50, 60, 70, 90] //sorted
var left = 0
var right = numbers.count - 1
var middle = 0

while left <= right {
    middle = (left + right) / 2
    
    if numbers[middle] == myFavourite {
        print("Found! Your favourite number at index: \(middle) with value: \(numbers[middle]) \n")
        break
    } else if numbers[middle] < myFavourite {
        print("The middle index \(middle) with value:  \(numbers[middle]) is too small")
        print("Please update left to: \(middle + 1) \n")
        
        left = middle + 1
    } else {
        print("The middle index \(middle) with value:  \(numbers[middle]) is too large")
        print("Please update right to: \(middle - 1) \n")
        
        right = middle - 1
    }
}
```
Outputs:
```
The middle index 5 with value: 20 is too small
Please update left to: 6
The middle index 8 with value: 50 is too large 
Please update right to: 7
Found! Your favourite number at index: 6 with value: 30
```

{{< admonition tip >}}
Notice that `left` is now `6` and `right` is `7` and mid is now `(6 + 7) / 2`
which is 6 *(integer division)*, and `6` is the correct index for our favourite number.
{{< /admonition >}}

Awesome! It only took `three (3)` lookups to finally located our favorite number.

Now let's write a function combined with the power of swift features to write a
clean version of a binary search algorithm.

#### The Binary search function

```swift
/// This binary search function will accept an array of items of type Int
/// and also a search value, It will then search for the index of
/// that value in the items and return the index if found or nill if not found
func binarySearch(for value: Int, in items: [Int]) -> Int? {
    var left = 0
    var right = items.count - 1
    var mid = 0
   
    while left <= right {
        mid = (left + right) / 2
        
        if items[mid] == value {
            return mid
            
        } else if items[mid] < value {
            left = mid + 1
            
        } else  {
            right = mid - 1
        }
    }
    return nil
}
```

##### Testing the function

Below we created a simple ordered `(sorted)` array to test the binary search function.

```swift
let numbers = [-2, 0, 1, 4, 10, 20, 30, 40, 50, 60, 70, 90] //sorted
let myFavourite = 30

if let index = binarySearch(for: myFavourite, in: numbers) {
    print("Index Found: \(index)")
} else {
    print("Your favourite number is: \(myFavourite) not in the numbers")
}

let myFavouriteTwo = 14
if let index = binarySearch(for: myFavouriteTwo, in: numbers) {
    print("Index Found: \(index)")
} else {
    print("Your favourite number is: \(myFavouriteTwo) not in the numbers")
}
```
Outputs
```
Index Found: 6
Your favourite number: 14 is not in the numbers
```


## conclusion

We have successfully built a binary search function that can be used to search a light of `integers`
I hope you enjoyed the reading. Report any typos or questions, and I will follow up!