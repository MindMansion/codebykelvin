---
title: "How to find index of an array element in Swift"
date: 2021-12-01T21:57:40+08:00
lastmod: 2022-01-01T16:45:40+08:00
draft: false
author: "Kelvin"
description: "How to find the index of array element in Swift."
featuredImage: "/learning-swift.png"

tags: ["Swift", "Basic"]
categories: ["Articles"]

lightgallery: true

---

<!--more-->

Swift standard library array is pack with lots of functionalities that help us mutate and
perform operations on arrays, and some of these methods includes:

## Methods

- firstIndex(where: )
- firstIndex(of: )
- first(where: )

### FirstIndex(where: )

The `firstIndex(where: )`  can be used to find and return the index of an array element and
returns nil if the index is not found.

```swift
let names = ["Smith", "Kelvin", "Wendy", "Mike"]

if let index = names.firstIndex(where: {$0 == "Wendy"}) {
    print(index)
}
```
`2`

### FirstIndex(of: )
Or we can also use the `firstIndex(of: )` method
```swift
if let index = names.firstIndex(of: "Smith") {
    print("index:", index)
}
```
`Index: 0`

### First(where: )

To return the actual element instead of the index, we can use the `first(where: )` method, this method
also return an optional value the element or `nil` if not found.

```swift
struct Rect: Identifiable {
    var id = UUID()
    var width: Double
    var height: Double
    
    func describe() -> String {
        "Width: \(self.width), Height: \(self.height)"
    }
}

let rects = [
    Rect(width: 25.0, height: 20.0),
    Rect(width: 125.0, height: 20.0),
    Rect(width: 25.0, height: 320.0)
]
```

#### Using `Rect` type example.

```swift
let rect = rects[2]

if let rect = rects.first(where: {$0.height == rect.height}) {
    print(rect.describe())
}
```
`Width: 25.0, Height: 320.0`

#### Find the rect index

```swift
if let rect = rects.firstIndex(where: {$0.height == rect.height}) {
    print(rect)
}
```
`2`