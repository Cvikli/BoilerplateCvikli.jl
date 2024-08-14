# BoilerplateCvikli.jl
**Enhance productivity** with simple boilerplate codes! 

These snippets could potentially belong to the Base module. However, only time will tell if they will be adopted by the Julia community.

## Install
```
] add BoilerplateCvikli
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

using BoilerplateCvikli: push_ifne!, findfirst_typed, idxI, @async_showerr


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
@show is extremely useful because it eliminates the need for parentheses. While this might seem minor, it's crucial for quick typing. Julia's most important debugging function should adopt this style as it is very fast to type. Of course, in other languages, you would use macros for this, but that introduces a significant amount of boilerplate code, which is a cognitive burden and should be reduced as much as possible.

That is why @sizes and @typeof are also extremely useful. It could be standardized by the community, though my focus is primarily on supporting my own goals.


Some of these boilerplates are so trivial that they're already on Julia Discourse. I've just copied some of them.

## Contribute
If you have any other useful boilerplate code that improves productivity, please don't hesitate to share! We help each other! ;)


## Other Productivity Tools
Here are some other productivity tools I recommend:

- The best stacktrace I am using: RelevanceStacktrace.jl. Reduce error search to ZERO! JuliaSyntax.jl will give us even more possibilities.
- I have a fork of the julia-vscode plugin that is also extremely useful; I cannot emphasize this enough. Sadly, Python cannot do this as well as Julia. - - This is actually the main reason Julia is the best language today.
- Sysimage creator that is also really great! It can precompile packages while keeping them modifiable from outside. As of Julia 1.9, this is less of a big deal.
- PkgResolver package that could be expanded and added to the sysimage, so it would automatically find and resolve package issues when using "add" and "dev". This project's goal is to reduce the problem of package resolving to just running one simple script.
- Also, there is ExtremeBoilerplate, which introduces type piracy issues to further improve the codebase. (However, if the specified package adopts the function, it won't cause type piracy. 😊)
- I will share more later on.


## Sidenote
It was a long journey for this package to get into the General registry, as it consists of snippets that eliminate boilerplate code, and some of them could also be used in startup.jl. Of course, some of them, like @display, @println, or @async_showerr, already cause dependencies, so they could be included. Nonetheless, the other part is similar to @show, so they are actually an important part of the ecosystem and could become an important part of the Base module as they get recognized by the community!


