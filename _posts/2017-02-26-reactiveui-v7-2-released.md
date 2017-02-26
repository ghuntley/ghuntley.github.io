---
title: ReactiveUI v7.2.0 released
date: '2017-02-26 15:00:00'
categories:
- reactiveui
- xamarin
summary: ''
layout: post
---

As part of this release we had [34 commits](https://github.com/reactiveui/reactiveui/compare/7.1.0...7.2.0) which resulted in [27 issues](https://github.com/reactiveui/ReactiveUI/issues?milestone=6&state=closed) being closed.


__All Platforms__

- [__#1282__](https://github.com/reactiveui/ReactiveUI/pull/1282) feat: a more flexible default view locator
- [__#1261__](https://github.com/reactiveui/ReactiveUI/pull/1261) feat: allow interaction handlers of any observable type
- [__#1255__](https://github.com/reactiveui/ReactiveUI/pull/1255) feat: add scheduling support to interactions
- [__#1283__](https://github.com/reactiveui/ReactiveUI/pull/1283) fix: add `UseInvariantCultureAttribute` and apply to relevant tests
- [__#1274__](https://github.com/reactiveui/ReactiveUI/pull/1274) fix: ensure synchronous command execution is lazy. Note that this is a potentially breaking change if your existing usage of synchronous commands is incorrect. See the issue for details.
- [__#1247__](https://github.com/reactiveui/ReactiveUI/issues/1247) fix: catch exceptions from `InvokeCommand`
- [__#1244__](https://github.com/reactiveui/ReactiveUI/issues/1244) fix: complete command execution only when pipeline completes
- [__#1235__](https://github.com/reactiveui/ReactiveUI/issues/1235) fix: `InvokeCommand` targets `ReactiveCommandBase`, not `ReactiveCommand`
- [__#1289__](https://github.com/reactiveui/ReactiveUI/pull/1289) perf: use shared, static observables to reduce allocations
- [__#1236__](https://github.com/reactiveui/ReactiveUI/issues/1236) perf: remove superfluous `AsObservable` calls in `ReactiveCommand`
- [__#1269__](https://github.com/reactiveui/ReactiveUI/pull/1269) test: add activation tests
- [__#1268__](https://github.com/reactiveui/ReactiveUI/pull/1268) style: tidy up and expand comments in activation code

__Xamarin Android__

- [__#1250__](https://github.com/reactiveui/ReactiveUI/pull/1250) feat: more flexible `WireUpControls` implementation 

__Xamarin Forms__

- [__#1270__](https://github.com/reactiveui/ReactiveUI/pull/1270) feat: synchronize `ViewModel` and `BindingContext` properties
- [__#1281__](https://github.com/reactiveui/ReactiveUI/pull/1281) fix: assign VM from correct thread in `RoutedViewHost`

__Housekeeping__

- [__#1180__](https://github.com/reactiveui/ReactiveUI/pull/1180) feat: enable unit test coverage/coveralls
- [__#1267__](https://github.com/reactiveui/ReactiveUI/pull/1267) style: tidy up comments for binding code
- [__#1263__](https://github.com/reactiveui/ReactiveUI/pull/1263) chore: failing to set the appveyor version should not be a fatal build error
- [__#1257__](https://github.com/reactiveui/ReactiveUI/pull/1257) chore: resolved gitlink wasn't working because pdbs/xml were not included because of a packaging defect
- [__#1252__](https://github.com/reactiveui/ReactiveUI/pull/1252) chore: rename _MobileLifecycle.cs_ to _SuspensionHost.cs_
- [__#1238__](https://github.com/reactiveui/ReactiveUI/pull/1238) chore: removed next-version definition

__Documentation__

- [__#1243__](https://github.com/reactiveui/ReactiveUI/pull/1243) docs: delete docs folder
- [__#1198__](https://github.com/reactiveui/ReactiveUI/issues/1198) docs: document pull-request merging guidelines/process
- [__#1197__](https://github.com/reactiveui/ReactiveUI/issues/1197) docs: document release process for contributors

### Where to get it
You can download this release from [nuget.org](https://www.nuget.org/packages/reactiveui/7.2.0)