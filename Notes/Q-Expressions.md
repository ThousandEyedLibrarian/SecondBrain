Q-expressions (quoted expressions) are unevaluated [[S-Expressions]] that represent code as data without immediate execution. 

Used in [[Lisp]]s.

## Syntax

- **Basic form**: `{expression}`
- **Quote operator**: `'expression` (shorthand for quote)
- **Examples**: `{+ 1 2}`, `'{hello world}`, `{if true 42 0}`

## Key Differences from S-Expressions

|S-Expression|Q-Expression|
|---|---|
|`(+ 1 2)` → `3`|`{+ 1 2}` → `{+ 1 2}`|
|Evaluated immediately|Stored as data|
|`()` parentheses|`{}` curly braces|

## Operations

- **eval**: Convert q-expression to s-expression and evaluate
    - `eval {+ 1 2}` → `3`
- **list**: Create q-expression from arguments
    - `list 1 2 3` → `{1 2 3}`
- **head/tail**: Access list elements
    - `head {a b c}` → `{a}`
    - `tail {a b c}` → `{b c}`