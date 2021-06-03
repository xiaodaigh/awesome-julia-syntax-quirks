# awesome-julia-syntax-quirks

##struct as function and other struct weirdness

```julia
#For those wondering, it's a clever trick to make it so that _GLOBAL_RNG has no constructors
struct _GLOBAL_RNG <: AbstractRNG
    global const GLOBAL_RNG = _GLOBAL_RNG.instance
end

julia> struct _Foo
           return nothing
       end
julia> const Foo = _Foo.instance
_Foo()


julia> fieldnames(_Foo)
()
julia> methods(_Foo)
# 0 methods for type constructor:


julia> begin
       struct Foo
           return 1
       end
       struct Bar
           return 2
       end
       end
1
julia> Bar
ERROR: UndefVarError: Bar not defined

julia> struct Foo 
           nothing
       end
julia> fieldnames(Foo)
(:nothing,)

julia> struct Bar
           1+1
       end
julia> fieldnames(Bar)
()

julia> no_constructor() = nothing
no_constructor (generic function with 1 method)
julia> struct Baz
           no_constructor()
       end

struct Foo
   function Foo end
end
```
