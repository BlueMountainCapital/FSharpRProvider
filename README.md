F# R Provider [![Build Status](https://api.travis-ci.org/fslaborg/RProvider.svg?branch=master)](https://travis-ci.org/fslaborg/RProvider/builds)
[![Nuget Version](https://buildstats.info/nuget/RProvider)](https://www.nuget.org/packages/RProvider/)
=======

<img align="right" src="https://github.com/fslaborg/RProvider/raw/master/docs/files/images/logo.png" alt="RProvider" />


An F# type provider for interoperating with [R](http://www.r-project.org/). For more information, see [detailed documentation with tutorials, examples and more](https://fslab.org/RProvider//). The following tutorials are a good place to start:

 - [Quickstart: Using Statistical Packages](https://fslab.org/RProvider//Statistics-QuickStart.html)
 - [Quickstart: Creating Charts](https://fslab.org/RProvider//Charts-QuickStart.html)
 - [Tutorial: Analysing Stock Prices](https://fslab.org/RProvider//tutorial.html)

What does it do?
----------------
The R Provider discovers R packages that are available in your R installation and makes them available as .NET namespaces underneath the parent namespace RProvider.  For example, the stats package is available as RProvider.stats.  If you open the namespaces you want to use, functions and values will be available as R.name.  For example, consider this F# interactive script:

```fsharp
#r "RProvider.dll"

open RProvider
open RProvider.``base``

let v = R.c(1,2,3)
```

This creates an R numeric vector containing 1,2,3, and names it v.  Note that we had to open the base namespace, since the function 'c' is part of that namespace.  You should also open namespace RProvider, because it contains some helper functions.

And because type providers are used by Visual Studio, Xamaring Studio and other IDEs, you will get intellisense for R functions.  You will also get compile-time type-checking that the function exists.

How to use it
-------------
Install using the [NuGet package](https://nuget.org/packages/RProvider/).  Many thanks to Mathias Brandewinder for producing the [FAKE](https://github.com/fsharp/FAKE) script to build the NuGet package, and to Steffen Forkmann for writing [FAKE](https://github.com/fsharp/FAKE).

There is a lot of info on how to use the provider on our [documentation page](https://fslab.org/RProvider//)

License
-------
RProvider is covered by the BSD license.

The library uses [RDotNet](https://github.com/rdotnet/rdotnet) which is also covered by the BSD license.

Pre-requisites
--------------
The R Provider requires an installation of R, downloadable from [here](http://cran.r-project.org/). 

On Windows, RProvider uses the R registry key `SOFTWARE\R-core` to locate the R binary directory, in order to load `R.dll`.  It will also locate `R.dll` if it is on the path.  If run from a 32-bit process, RProvider will use the 32-bit R.DLL, and if run from a 64-bit process, it will load the 64-bit version.

On Mac and Linux, you need to install 64 bit version of Mono, setup Xamarin Studio to run F# Interactive in 64 bit and create a configuration file `~/.rprovider.conf` to tell the R provider how to start its server process in 64 bit mode. For detailed documentation [see the R provider Mac/Linux page](https://fslab.org/RProvider//mac-and-linux.html).

If you are using R 2.15 or later, you should not try to load the RProvider inside a script that is passed to FSI via the --use flag.  It seems that something about the way R initializes causes it to hang in that context.  Works fine if you load later.

For compilation you will need VS2012 / F# 3.0 or later.  For runtime you'll need .NET 4.5.
