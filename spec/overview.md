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
- `(variable | pred)` _:: A `Rule`, compile time assertion._
- `[pattern-out | pattern-in :: variable-bindings&predicates ]` _:: A `List-builder`, a function taking a value_ (see https://ghc.gitlab.haskell.org/ghc/doc/users_guide/exts/monad_comprehensions.html)
- `{variable | variable-bindings&predicates}` _:: A `Set-Builder`, a function taking a set_

## Types Sets and values
The type system depends on dealing with explicit `Sets`, and an algebra between `Sets`.



a set containing a type is distinct from the type itself
```yaml
{{true} maybe} ≠ {true false}
```
A set indexed by a number is a subset of 


Names can be created in two ways, 
- `alias : value`   :: an alias
- `rename ← value` :: a rename

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
boolean2 ← {true false}
bool2    ← {true false}

not_(boolean2 = {true false})
not_(boolean2 = bool2)
```

a set can be pulled out with pattern matching
```yaml
not_(bool2 ∩ {maybe} = {true false maybe}

(bool2_'a :: 'a )_bool2 ∩ {maybe} = {true false maybe}

(boolean2_'a :: 'a)_boolean2 = (bool2_'b :: 'b)_bool2
```

## Pattern Matching
Pattern matching can be done by preceding braces with `?`, variables are distinguished by a preceding tick `'`.
```
?('a)   :# identiy function
('a | 1 = :? 10
 '_       :? 20
)
('a | 'a ∊ {1 2 3} ∊ u8 :? 0
 '_                     :? 1
)
```

## Function definition
```
id : ?('a :: 'a)
mean : ?('a :: 'a . /_+ % #)

mean`([Array:num num]:fn) : /_+ % #
mean : /_+ % #
```







