---
title: "How to quickly generate array in Swift"
date: 2021-12-01T21:57:40+08:00
lastmod: 2022-01-01T16:45:40+08:00
draft: false
author: "Kelvin"
description: "How to quickly generate an array of any type in Swift."
featuredImage: "/learning-swift.png"

tags: ["Swift", "Basic"]
categories: ["Articles"]

lightgallery: true

---

<!--more-->

Sometimes you want to quickly generate an array in your swift code
without having to manually type in the elements, you can quickly
do that in Swift using the `repeating method`

## Generate array of 20 zeros

```swift
let twentyZeros = Array(repeating: 0, count: 20)
print(twentyZeros)
```
Output: `[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]`

## Generating array of 50 strings

```swift
let arrayOfString = Array(repeating: "City", count: 50)
```

This same method can be applied to any type in swift such as objects,
just provide whatever you want to generate, and specify the `count`.