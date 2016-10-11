---
title: Xamarin Application Semantic Versioning
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
One of the unique things about Xamarin is the ability to share a large chunk of code between platforms. 

This vies as I haven't seen much discussion about how to express this in Semantic Versioning (SemVer), 

.NET Core is a platform of NuGet packages, of frameworks and distributed as a unit. Each of these platform layers can be versioned separately for product agility and to accurately describe product changes. While there is significant versioning flexibility, there is a desire to version the platform as a unit to make the product easier to understand.

## Decision Tree

**MAJOR when:**

- directed by the business as per your sales and marketing strategy

**MINOR when:**

- any shared logic change (i.e. changes in portable class library)

**PATCH when:**

- any user interface change (i.e. pixel pushing existing or adding new ui)
- any core application change (i.e. upgrading analytics dependency) 
- any platform service change (i.e. `CoreLocationService` implementation of `ILocationService`)