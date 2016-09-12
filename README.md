# FusionTasks
![FusionTasks](https://raw.githubusercontent.com/kekyo/FSharp.Control.FusionTasks/master/Images/FSharp.Control.FusionTasks.128.png)

## Status
* NuGet Package (F# 2.0): [![NuGet FusionTasks (F# 2.0)](https://img.shields.io/nuget/v/FSharp.Control.FusionTasks.FS20.svg?style=flat)](https://www.nuget.org/packages/FSharp.Control.FusionTasks.FS20)
* NuGet Package (F# 3.0): [![NuGet FusionTasks (F# 3.0)](https://img.shields.io/nuget/v/FSharp.Control.FusionTasks.FS30.svg?style=flat)](https://www.nuget.org/packages/FSharp.Control.FusionTasks.FS30)
* NuGet Package (F# 3.1): [![NuGet FusionTasks (F# 3.1)](https://img.shields.io/nuget/v/FSharp.Control.FusionTasks.FS31.svg?style=flat)](https://www.nuget.org/packages/FSharp.Control.FusionTasks.FS31)
* NuGet Package (F# 4.0): [![NuGet FusionTasks (F# 4.0)](https://img.shields.io/nuget/v/FSharp.Control.FusionTasks.FS40.svg?style=flat)](https://www.nuget.org/packages/FSharp.Control.FusionTasks.FS40)
* Continuous integration: [![AppVeyor FusionTasks](https://img.shields.io/appveyor/ci/kekyo/fsharp-control-fusiontasks.svg?style=flat)](https://ci.appveyor.com/project/kekyo/fsharp-control-fusiontasks)
* Gitter: [![Gitter FusionTasks](https://badges.gitter.im/kekyo/FSharp.Control.FusionTasks.svg)](https://gitter.im/kekyo/FSharp.Control.FusionTasks?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

## What is this?
* F# Async workflow <--> .NET Task easy seamless interoperability library.
* Sample codes (F# side):

``` fsharp
let asyncTest = async {
  use ms = new MemoryStream()

  // FusionTasks directly interpreted System.Threading.Tasks.Task class in F# async-workflow block.
  do! ms.WriteAsync(data, 0, data.Length)
  do ms.Position <- 0L

  // FusionTasks directly interpreted System.Threading.Tasks.Task<T> class in F# async-workflow block.
  let! length = ms.ReadAsync(data2, 0, data2.Length)
  do length |> should equal data2.Length
}
```

* Sample codes (C# side):

``` csharp
using System.Threading.Tasks;
using Microsoft.FSharp.Control;

public async Task AsyncTest(FSharpAsync<int> asyncIntComp)
{
  // FusionTasks simple usage F#'s Async<unit> direct awaitable.
  await FSharpAsync.Sleep(500);
  Console.WriteLine("Awaited F# async function (unit).");

  // FusionTasks simple usage F#'s Async<int> direct awaitable.
  var result = await asyncIntComp;
  Console.WriteLine("Awaited F# async function: Result=" + result);
}
```

## Features
* Easy interoperability .NET Task <--> F#'s Async.
* F# async workflow block now support direct .NET Task handle with let!, do! and use!.
* .NET (C# async-await) now support directly F#'s Async.
* SyncronizationContext capture operation support (F#: Configure method / .NET (C#) AsAsyncContext method)

## Benefits
* Easy interoperability, combination and relation standard .NET OSS packages using Task and F#'s Async.
* F# 2.0, 3.0, 3.1 and 4.0 with .NET 4.0/4.5/.NET Core 1.0 include PCL Profile 7/47/78/259.
* Ready for LINQPad 5.

## Environments
* .NET Framework 4.0/4.5
* .NET Core 1.0 (Only F# 4.0)
* .NET Framework Portable class library (Profile 7/47/78/259)
* F# 2.0, 3.0, 3.1, 4.0 (NuGet package separated, choose one)

## How to use
* Search NuGet package and install "FSharp.Control.FusionTasks.FS??". You must select F# version.
* F# use, autoopen'd namespace "FSharp.Control". "System.Threading.Tasks" is optional.
* C# use, using namespace "System.Threading.Tasks". "Microsoft.FSharp.Control" is optional.

## Additional resources
* Source codes available only FSharp.Control.FusionTasks.FS3PCL47 project.
* The "Continuation Passing Style" basics and provide seamless interoperability .NET Task and F# Async workflow implicit conversion technics. "NLNagoya 2016" conference session slides. (Composed blog post, sorry Japanese only) http://www.kekyo.net/2016/04/17/5804

## TODO
* Improvements more easier/effective interfaces.

## License
* Copyright (c) 2016 Kouji Matsui
* Under Apache v2 http://www.apache.org/licenses/LICENSE-2.0

## History
* 0.9.3:
  * Fixed nuspec frameworkAssemblies.
* 0.9.2:
  * Add package targetFramework.
  * Updated RelaxVersioner.
* 0.9.1:
  * Remove strongly-signed (Unit test doesn't work...)
  * Omit synchronizers (AsyncLock, AsyncLazy). Thats moving to FSharp.Control.AsyncPrimitives project (https://github.com/kekyo/FSharp.Control.AsyncPrimitives).
  * Add target dnxcore50 into F# 4.0 (for .NET Core 1.0)
  * Source codes and documents bit changed.
* 0.5.8:
  * Add strongly-signed.
* 0.5.7:
  * Add PCL Profile 7.
* 0.5.6:
  * Add PCL Profile 78.
  * Fixed minor PCL moniker fragments.
* 0.5.5:
  * Fixed version number.
  * Fixed icon image url.
* 0.5.4:
  * Auto open FSharp.Control.
  * Manage AppVeyor CI.
* 0.5.3: Implement awaiter classes.
* 0.5.2: Add dependency assemblies.
* 0.5.1: NuGet package support.
