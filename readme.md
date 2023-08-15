FreeMoq
===

![FreeMoq](/assets/img/moq-icon.png)

[![Nuget](https://img.shields.io/nuget/v/FreeMoq?logo=nuget&style=default)](https://www.nuget.org/packages/FreeMoq)
![Nuget](https://img.shields.io/nuget/dt/FreeMoq?logo=nuget&style=default&color=blue&label=Downloads)
[![The Standard Community](https://img.shields.io/discord/934130100008538142?style=default&color=%237289da&label=The%20Standard%20Community&logo=Discord)](https://discord.gg/vdPZ7hS52X)

Considerations
===

This is just a fork of the [moq project](https://github.com/moq/moq).<br/>
The goal is to bring in all the stuff developed in the main project, leaving out things like [SponsorLink](https://github.com/moq/moq/issues/1374) for as long as the license supports it.<br/>
- Your privacy is valued, therefore we do not intend to obtain any personal information from your machine.<br/>
- Your time is valued, so we don't intend to purposely degrade your build.<br/>
- Your effort is valued, so we don't intend to pollute the output with non-test related messages.<br/>
- The FOSS philosophy is respected, and at no time will you be charged for using this tool.

BTW: **Be obedient**, and **DO NOT** make any donations to my ETH wallet! *0x5cDF219375d00FbDB55de48b72Aef730F65ab767*

moq
===

<!-- #content -->
The most popular and friendly mocking library for .NET

```csharp
  var mock = new Mock<ILoveThisLibrary>();

  // WOW! No record/replay weirdness?! :)
  mock.Setup(library => library.DownloadExists("2.0.0.0"))
      .Returns(true);

  // Use the Object property on the mock to get a reference to the object
  // implementing ILoveThisLibrary, and then exercise it by calling
  // methods on it
  ILoveThisLibrary lovable = mock.Object;
  bool download = lovable.DownloadExists("2.0.0.0");

  // Verify that the given method was indeed called with the expected value at most once
  mock.Verify(library => library.DownloadExists("2.0.0.0"), Times.AtMostOnce());
```

Moq also is the first and only library so far to provide Linq to Mocks, so that the 
same behavior above can be achieved much more succinctly:

```csharp
  ILoveThisLibrary lovable = Mock.Of<ILoveThisLibrary>(l =>
    l.DownloadExists("2.0.0.0") == true);

  // Exercise the instance returned by Mock.Of by calling methods on it...
  bool download = lovable.DownloadExists("2.0.0.0");

  // Simply assert the returned state:
  Assert.True(download);
  
  // If you want to go beyond state testing and want to 
  // verify the mock interaction instead...
  Mock.Get(lovable).Verify(library => library.DownloadExists("2.0.0.0"));
```

You can think of Linq to Mocks as "from the universe of mocks, give me one whose behavior 
matches this expression".

Check out the [Quickstart](https://github.com/moq/moq/wiki/Quickstart) for more examples!

<!-- #content -->

## What?

Moq (pronounced "Mock-you" or just "Mock") is the only mocking library for .NET developed from scratch to take full advantage of .NET Linq expression trees and lambda expressions, which makes it the most productive, type-safe and refactoring-friendly mocking library available. And it supports mocking interfaces as well as classes. Its API is extremely simple and straightforward, and doesn't require any prior knowledge or experience with mocking concepts.

## Why?

The library was created mainly for developers who aren't currently using any mocking library (or are displeased with the complexities of some other implementation), and who are typically [manually writing their own mocks](https://web.archive.org/web/20200920165817/http://blogs.clariusconsulting.net/kzu/mocks-stubs-and-fakes-its-a-continuum/) (with more or less "fanciness"). Most developers in this situation also happen to be [quite pragmatic and adhere to state](https://web.archive.org/web/20200414170510/http://blogs.clariusconsulting.net/kzu/state-testing-vs-interaction-testing/) (or classic) TDD. It's the result of feeling that the barrier of entry from other mocking libraries is a bit high, and a simpler, more lightweight and elegant approach is possible. Moq achieves all this by taking full advantage of the elegant and compact C# and VB language features collectively known as LINQ (they are not just for queries, as the acronym implies).

Moq is designed to be a very practical, unobtrusive and straight-forward way to quickly setup dependencies for your tests. Its API design helps even novice users to fall in the "pit of success" and avoid most common misuses/abuses of mocking. 

When it was conceived, it was the only mocking library that went against the generalized and somewhat unintuitive (especially for novices) Record/Replay approach from all other libraries (and [that might have been a good thing](https://web.archive.org/web/20200920165939/http://blogs.clariusconsulting.net/kzu/whats-wrong-with-the-recordreplyverify-model-for-mocking-frameworks/) ;)).

Not using Record/Replay also means that it's straightforward to move common expectations to a fixture setup method and even override those expectations when needed in a specific unit test.

You can read more about the "why" and see some nice screenshots at [kzu's blog](https://web.archive.org/web/20200920164302/http://blogs.clariusconsulting.net/kzu/why-do-we-need-yet-another-net-mocking-framework/).

## Where?

See our [Quickstart](https://github.com/moq/moq/wiki/Quickstart) examples to get a feeling of the extremely simple API and install from [NuGet](http://nuget.org/packages/moq).

Read about the announcement at [kzu's blog](https://web.archive.org/web/20201130233544/http://blogs.clariusconsulting.net/kzu/linq-to-mock-moq-is-born/). Get some background on [the state of mock libraries from Scott Hanselman](http://www.hanselman.com/blog/MoqLinqLambdasAndPredicatesAppliedToMockObjects.aspx).

In-depth documentation is being added to the [documentation website](http://moq.github.io/moq/).


## Who?

Moq was originally developed by [Clarius](http://www.clariusconsulting.net), [Manas](http://www.manas.com.ar) and [InSTEDD](http://www.instedd.org).

Moq uses [Castle DynamicProxy](http://www.castleproject.org/projects/dynamicproxy/) internally as the interception mechanism to enable mocking.

<!-- #features -->

## Features at a glance
Moq offers the following features:
* Strong-typed: no strings for expectations, no object-typed return values or constraints
* Unsurpassed VS IntelliSense integration: everything supports full VS IntelliSense, from setting expectations, to specifying method call arguments, return values, etc.
* No Record/Replay idioms to learn. Just construct your mock, set it up, use it and optionally verify calls to it (you may not verify mocks when they act as stubs only, or when you are doing more classic state-based testing by checking returned values from the object under test)
* VERY low learning curve as a consequence of the previous three points. For the most part, you don't even need to ever read the documentation.
* Granular control over mock behavior with a simple [MockBehavior](https://www.fuget.org/packages/Moq/4.16.1/lib/netstandard2.1/Moq.dll/Moq/MockBehavior) enumeration (no need to learn what's the theoretical difference between a mock, a stub, a fake, a dynamic mock, etc.)
* Mock both interfaces and classes
* Override expectations: can set default expectations in a fixture setup, and override as needed on tests
* Pass constructor arguments for mocked classes
* Intercept and raise events on mocks
* Intuitive support for ```out/ref``` arguments

We appreciate deeply any feedback that you may have! Feel free to participate in the [chat], or report an issue in the [issue tracker].

 [chat]:
 https://discord.gg/8PtpGdu
 "Moq channel on Discord"

 [issue tracker]:
 https://github.com/moq/moq/issues
 "Moq issue tracker on GitHub"

<!-- #features -->
