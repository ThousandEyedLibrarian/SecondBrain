S-expressions (symbolic expressions) are a notation for nested [[Array Lists]] structures, originally developed for [[Lisp]] programming languages.

> "*To store the program we will need to create an internal list structure that is built up recursively of numbers, symbols, and other lists. In Lisp, this structure is commonly called an S-Expression standing for Symbolic Expression. We will extend our `lval` structure to be able to represent it. 
> 
> The evaluation behaviour of S-Expressions is the behaviour typical of Lisps, that we are used to so far. To evaluate an S-Expression we look at the first item in the list, and take this to be the operator. We then look at all the other items in the list, and take these as operands to get the result.*" - buildyourownlisp.com

### Example Syntax
```lisp
(define (square x)
  (* x x))

(map square '(1 2 3 4))
; Returns: (1 4 9 16)
```

## [[Q-Expressions]]


See also:
- [[Designing a Programming Language]]