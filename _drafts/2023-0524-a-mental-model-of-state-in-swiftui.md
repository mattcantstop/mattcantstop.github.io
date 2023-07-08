---
layout: post
title: "A mental model of SwiftUI application state"
date: 2023-05-24
description: "I am building an iOS application and wanted to write up my understanding of _state_ in SwiftUI."
---

### The confusing bits about state in SwiftUI

One aspect that has confused me in SwiftUI is that there seems to be very little connecting the declaration of a variable in one view, or in the `.environmentobject`, and the use of that variable in another view. The naming conventions didn't seem clear to me. I want to explore this in a sample application to understand this better. An example of my confusion is _can I declare an `.environmentObject` in one view and then access it in another view with a different variable name? How does it trigger accessing that object, based on the variable name? 

## A filtering question

Is it simple? Is this a boolean, or just one instance of a piece of data, and it won't have nested properties or anything like that? 

## The simple

Simple types: 

- Bool
- Array
- String

### @AppStorage

- @AppStorage - adding data to overall App Storage, only one

### @SceneStorage

- @SceneStorage - adding data to the SceneStorage, based on scene

### @State and @Binding

- @State - declaration of a watchable State object
- @Binding - accessign the declared @State object, accessed by $<var> with the `$` sign. 

## The complex

These properties are more complex in nature. You maybe be storing larger objects, and they go past the simple boolean types. 

- Class
- ViewModel
- ObservedObject

### @StateObject

- @StateObject - declaration
- @ObservedObject - accessing the declared @StateObject
- Use: when it is localized. Where this comes into play is this requires you to hand down the object to child views in order to share the data. For that reason this wouldn't be something you use broadly, as it's tedious to share this for each view. 
- Good rule of thumb is to never use an intiatilizer when you have an ObservableObject. NEED TO LOOK INTO THIS MORE ❗❗️❗️️
- In example a Player() object that keeps track of a track playing was recreated whenever a parent view is reloaded. When the player was changed to a @StateObject the state object variable was held outside the view and reused. 

### `.environmentObject()

- .environmentObject() - declaration
- @EnvironmentObject - accessing the declared .environmentObject()
- Use: one intance, used throughout potentially all views. An example of this use case is when you have one logged in user at a time. It makes sense to add this to the environment. It would be available everywhere, and would simply the application. 
- 








### Object instantiation 

Object instantiation, and specifically async calls during instantiation, is only somewhat related, but related in the issues I am encountering in my app. I think I want to first understand state in a sample app, then potentially move to how to create objects well. 
