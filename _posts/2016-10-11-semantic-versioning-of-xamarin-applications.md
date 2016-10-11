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
One of the unique things about Xamarin is the ability to share large chunks of code between all of the mobile platforms. This provides an unique opportunity to version mobile applications as a complete unit reglardless of the destination app store or mobile platform. 

A Xamarin application typically consists of a core library where all the business logic is stored and tiny per-platform library implementations of non-portable services (i.e. `CoreLocationService : ILocationService`) and finally the actual applications itself.

Which can be expressed using the <a href="http://semver.org/">Semantic Versioning (SemVer)</a> standard as follows:

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Here&#39;s my recommendations for SemVer / versioning <a href="https://twitter.com/hashtag/Xamarin?src=hash">#Xamarin</a>. applications. &gt;$owned-by-marketing.$pcl-change.$platform-change.$buildepoch&lt;</p>&mdash; Geoffrey Huntley (@GeoffreyHuntley) <a href="https://twitter.com/GeoffreyHuntley/status/785657050432798720">October 11, 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

## Scheme

MAJOR.MINOR.PATCH.META aka BUSINESS.NETSTANDARD/PCL.PLATFORM.BUILDSTAMP

## Decision Tree

When determining what to increment when there are multiple changes, choose the highest kind of change and reset the suffix numbers back to zero. The MAJOR number is owned by the business and should only be incremented as directed as per your sales and marketing plan.

**MAJOR when:**

- directed by the business as per your sales and marketing strategy

**MINOR when:**

- any shared logic change (i.e. changes in portable class library) that isn't able to be shared across all plaforms

**PATCH when:**

- any non-portable user interface change (i.e. pixel pushing native ui or changing custom renderer)
- any core application change (i.e. upgrading platform analytics dependency) 
- any platform service change (i.e. `CoreLocationService` implementation of `ILocationService`)

**META when:**

- every time a new build is produced
