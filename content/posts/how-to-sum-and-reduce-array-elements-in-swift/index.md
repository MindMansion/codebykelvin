---
title: "How to sum and reduce array elements in Swift"
date: 2021-12-11T21:57:40+08:00
lastmod: 2022-01-01T16:45:40+08:00
draft: false
author: "Kelvin"
description: "How to quickly reduce your swift array to a single value."
featuredImage: "/learning-swift.png"

tags: ["Swift", "Basic"]
categories: ["Articles"]

lightgallery: true

---

<!--more-->

Sometimes you want to reduce `(sum)` the values of an array
to a single final value in your swift code, this can easily be achieved
by using the `Array reduce` method.

## Sum array of Integers

```swift
let twenty20 = Array(repeating: 20, count: 20)

let sum = twenty20.reduce(0, +)
print(sum)
```
Output:`400`

```swift
let myNumbers = [20, 50, 10, -1, 0, 500]
let sum = myNumbers.reduce(0, +)
```

