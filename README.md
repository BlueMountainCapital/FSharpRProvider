![logo](https://www.bluemountaincapital.com/media/logo.gif)
F# R Provider
=======
An F# type provider for interoperating with [R](http://www.r-project.org/).

What does it do?
================
The R Provider discovers R packages that are available in your R installation and makes them available as .NET namespaces underneath the parent namespace RProvider.  For example, the stats package is available as RProvider.stats.  If you open the namespaces you want to use, functions and values will be available as R.name.  For example, consider this F# interactive script:

````
#r "RProvider.dll"

open RProvider
open RProvider.``base``

let v = R.c(1,2,3)
````

This creates an R numeric vector containing 1,2,3, and names it v.  Note that we had to open the base namespace, since the function 'c' is part of that namespace.  You should also open namespace RProvider, because it contains some helper functions.

And because type providers are used by the Visual Studio IDE, you will get intellisense for R functions.  You will also get compile-time type-checking that the function exists.

How to use it
=============
There is a lot of info on how to use the provider on our [how to page](https://github.com/BlueMountainCapital/FSharpRProvider/wiki/How-To).

For other information, check out the other pages on the [wiki](https://github.com/BlueMountainCapital/FSharpRProvider/wiki).

License
=======
FSharpRProvider is covered by the BSD license.

The library uses [RDotNet](http://rdotnet.codeplex.com/) which is also covered by the BSD license.

Pre-requisites
==============
The R Provider requires an installation of R for Windows, downloadable from [here](http://cran.cnr.berkeley.edu/bin/windows/base/).  RProvider uses the R registry key SOFTWARE\R-core to locate the R binary directory, in order to load R.dll.  It will also locate R.dll if it is on the path.  If run from a 32-bit process, RProvider will use the 32-bit R.DLL, and if run from a 64-bit process, it will load the 64-bit version.

For compilation you will need VS2012 RC (or RTM once it comes out on August 15th).  For runtime you'll need .NET 4.5.
