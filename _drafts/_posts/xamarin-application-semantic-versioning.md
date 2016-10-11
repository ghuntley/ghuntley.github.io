---
title: Semantic Versioning of Xamarin Applications
date: '2016-10-11 01:54:00'
categories:
- xamarin
- semver
- devops
- xamarin ios
- xamarin android
- uwp
summary: ''
layout: post
---
One of the unique things about Xamarin is the ability to share a large chunk of code between all of the mobile platforms which provides an unique opportunity to version mobile applications as a complete unit. 

A Xamarin application typically consists of a core library where all the business logic is stored and tiny per-platform library implementations of non-portable services (i.e. `CoreLocationService : ILocationService`) and finally




.NET Core is a platform of NuGet packages, of frameworks and distributed as a unit. Each of these platform layers can be versioned separately for product agility and to accurately describe product changes. While there is significant versioning flexibility, there is a desire to version the platform as a unit to make the product easier to understand.

## Scheme

MAJOR.MINOR.PATCH.META

## Decision Tree

**MAJOR when:**

- directed by the business as per your sales and marketing strategy

**MINOR when:**

- any shared logic change (i.e. changes in portable class library) that isn't related to the user interface.

**PATCH when:**

- any user interface change (i.e. pixel pushing existing or adding new ui)
- any core application change (i.e. upgrading analytics dependency) 
- any platform service change (i.e. `CoreLocationService` implementation of `ILocationService`)

**META when:**

- every time a new build is produced