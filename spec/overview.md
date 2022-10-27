# **Dubious** basic overview
Some of these may have minor exceptions but they give an overal idea of what the visual language of the syntax is.


## Reseved Keywords
Reserved kewords start with `:`
```
:in
:for
:end
```
but in the initial design this is to be avoided.

## Braces
- `(a b c)` Round braces => a single `Expr`ession.
- `[a b c]` Square braces => __ordered__ `List` of homogeneous members.
- `{a b c}` Curly braces => a __finite__ `Set` of heterogeneous members.

## Value tokens
- `(a + b)` Values are separated by spaces. `(`, `a`, `+`, `b`, `)` are distinct tokens.
- `(a+b)` This is not equivalent to the above, it will be three tokens `(`, `a+b`, `)`.

## Brace Splitting Pipe
- `(variable | pred)` __:: A `Rule`, compile time assertion._
- `[variable | variable-bindings&predicates ]` _:: A `List-builder`, order matters_
- `{variable | variable-bindings&predicates .. optional-max-set}` _:: A `Set-Builder`, default-max-set is the All-Set_

## Types Sets and values
The type system depends on dealing with explicit sets, and an algebra between sets.

Sets `splat` into sets they are nested in.
```yaml
{{true false} maybe} = {true false maybe}
```
A set indexed by a number is a subset of 


Names can be created in two ways, 
- `alias : value` :: an alias
- `rename :- value` :: a rename

An alias is structuraly typed
```yaml
boolean : {true false}
bool    : {true false}
boolean = {true false}
boolean = bool
t : true
bool = {t false}
```

with sets that are aliased, they splat into sets they have been nested into
```yaml
{bool maybe} = {true false maybe}
```

A rename wraps the type making it act like a unique value
```yaml
boolean2 :- {true false}
bool2    :- {true false}
not_(boolean2 = {true false})
not_(boolean2 = bool2)
```

It also no longer splats, unless pulled out
```yaml
not_({bool2 maybe} = {true false maybe})
{ bool2.?{bool2_'a :: 'a} maybe } = {true false maybe}
```






