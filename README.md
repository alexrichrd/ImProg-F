# ImProg-F

Implementation of the functional programming language **F** using Haskell.

## Motivation

This group project was part of the practical *Implementation of Programming Languages*
at the Ludwig-Maximilians-Universität in Munich (winter semester 2021/22).
It introduced the participants to basic principles of formal languages,
functional programming, parsing, compiler construction, and abstract machines.

## Getting started

### Requirements
- [Haskell Tool Stack](https://docs.haskellstack.org/en/stable/README/) (recommended)
- [GHC](https://www.haskell.org/downloads/) (only required if building without Stack)

Clone the repository and navigate into it:

```bash
git clone https://github.com/alexrichrd/ImProg-F.git
cd ImProg-F
```

## Build & execution with Stack

This project uses Stack with a pinned LTS resolver. Stack will automatically
download and use a compatible GHC version if necessary.

Build and run the project using:

```bash
stack build
stack run improg
```

The interpreter then waits for input from standard input.

## Alternative: building with Cabal

If `cabal-install` is available on your system and a compatible GHC version is
installed, the project can also be built using:

```bash
cabal build
cabal run improg
```

## General Usage

- Every F program must contain a definition `main = ...;`
- `main` is the only (lazily) evaluated expression
- Local definitions are possible but restricted to value definitions
- See the `F_grammar.txt` file for a detailed description of the language

### Example usage

After starting the interpreter with

```bash
stack run improg
```

enter an F program directly into the terminal and finish input with an empty line
(or EOF).

Example: Gauss’s Easter algorithm

```text
main     = easter year;
mod a b  = a - ((a / b) * b);
easter y = let  a = mod y 19;
                b = mod y 4;
                c = mod y 7;
                M = 24;
                hd = (19 * a) + M;
                d = mod hd 30;
                N = 5;
                he = (2 * b) + (4 * c) + (6 * d) + N;
                e = mod he 7;
                res = (22 + d + e)
                in if (31 < res)
                    then (((res - 31) * 100) + 4)
                    else ((res * 100) + 3);
year     = 2022;
```

Result:

```text
1704
```

### Not supported
- Structured or enumerated types (and therefore no pattern matching)
- Lambda expressions and higher-order functions
- Tail recursion
- Error handling for infinite recursion

## Supported flags

- `tokens`
- `ast`
- `instructions`
- `states`

Use flags to print generated tokens, the abstract syntax tree,
MF instructions, and intermediate MF states during program execution.

```bash
stack run improg -- -flagName
```

## References

See the [homepage](https://uni2work.ifi.lmu.de/course/W21/IfI/ImProg)
of the practical for more information.
