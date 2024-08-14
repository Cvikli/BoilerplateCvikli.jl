# BoilerplateCvikli.jl
**Enhance productivity** with simple boilerplate codes! 

These snippets actually could belong to the Base module. But time will tell if they will be used by the Julianners community and then they get adopted!  

## Install
```
using Pkg; Pkg.add(url="https://github.com/Cvikli/BoilerplateCvikli.jl")
using BoilerplateCvikli
```
or from this repository: 
```
] add https://github.com/Cvikli/BoilerplateCvikli.jl
using BoilerplateCvikli
```


## Features
- `@sizes`: Very simple size print
- `@typeof`: Simplest type print
- `@display` and `@println`: Simplest print
- `@dtime`: Simple execution time measurement
- `@clear_line`: Clear above terminal line
- `@async_showerr` and `@asyncsafe`: Error-handling for async operations
- `findfirst_typed`: Typesafe find first
- `idxI`: Extract elements at specific index from array of arrays
- `push_ifne!`: Push if not exist. 



## Quick Overview

```julia
using BoilerplateCvikli

a2 = [100,3,4,2]
a1 = (randn(Float32, 2,4,2),a2,(rand(1:10,100,5), randn(Float32,100,9)))

# UNIVERSAL sizes! Extremely handy in any situation! 
@sizes a1 

# macro typeof! It's as simple as @show!
@typeof a1

# Beautiful print!
@display q = randn(6,3)

using BoilerplateCvikli: push_ifne!, findfirst_typed, idxI, @get, @async_showerr


push_ifne!(a2, 3)
push_ifne!(a2, 4) # Push if not exists
@show a2

# findfirst with that 'Nothing' is just a big antipattern, let's just use this instead! I love type stability, and also compilers so whynot use unstable codes with little to no drawbacks.
@show findfirst_typed(==(7), a2)  # ==(7)  is actually v->v==7
# I think actually findfirst should be renamed to findfirst_safe or something that means it is a different findfirst than in any other languages. (Of course, it is beautiful stuff, but sounds like an antipattern)

# and never forget that we have @edit which is one of the most powerful tools of Julia too!

a3 = idxI.(a1, 1) # of course it isn't that beautiful syntax... but isn't used frequently anyways! It also works with Vector{Matrix[Float32]} or anything...
@typeof a3
@sizes a3

@get tracked.[:y, :y]   # get multiple values from dict like from the arrays in a beautiful way!

fn2(x) = begin
  println(x)
  sleep(x)
end

@async fn2("0.2") # CAUTION! Errors in @async are not printed anywhere, things just die... Silent errors are the deadliest enemies. Has to be zeroed! I guess everyone has been there already with @async and everyone simply fixed for themselves.
@async_showerr fn2(0.1)
try 
  @async_showerr fn2("0.2")
catch e
  println("The error actually catchable!")
  bt = catch_backtrace()
  showerror(stderr, e, bt)
  println()
end
sleep(1.3)
println()
println("These things actually make everything extremly fast to debug!")
```

## Why Use BoilerplateCvikli?
`@show` is extremly useful because it eliminates the need for parentheses. While this might seem minor, it's crucial for quick typing. Julia's most important debugging function should adopt this style as it's super fast to type. (Of course in other languages you use macros for this, but also that gives a crazy amount of boilerplate code, which is a cognitive burden and should be reduced as much as possible.) 
That is why `@sizes` and `@typeof` is also extremely useful. 
(Ofc, it could be standardised by community, as this is mainly for support my own goal.)


Some of these boilerplates are so trivial, that they're already on discourse.julia. I've just copied some of them.

## Contribute
If you have any other useful boilerplate code that improves productivity please don't hesitate to share! 
We help each other! ;)


## Other Productivity Tools
Here are some other productivity tools I recommend:
- Best stacktrace I am using: https://github.com/Cvikli/RelevanceStacktrace.jl Reduce the error search to ZERO! JuliaSyntax.jl will give us even more possibilities.
- I will share a lot more. 
- I have a fork of the julia-vscode plugin, that is also extremly useful, I cannot emphasize this. Sadly Python cannot do this this well like julia, actually this is the main reason julia is the best language of today. 
- sysimage creator that is also really great! Also that can precompile packages while keeping it modifiable from outside. As of julia 1.9 version is out, this is less of a big deal.
- PkgResolver package, that could be expanded and added to sysimage so it would automatically find the problem and resolve packages added with "add" and "dev". This project's goal is to reduce the problem of package resolving to just running one simple script.    


## Sidenote
It took really long journey till this package get into the General registry as it is sort of snippets that spares Boilerplate codes and some of them could be also used as startup.jl. Of course some of them like `@display`, `@println` or `@async_showerr` and others, already causes dependency so it could get in. 
None the less, the other part is similar to `@show`, so they are actually important part of the ecosystem and could be important part of the Base module as it gets recognized by the community! 


