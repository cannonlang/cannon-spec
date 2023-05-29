# Cannon Grammars

This folder describes the grammars used by the Cannon Language, written in a subset of ABNF. 

The syntax of the grammar specifications is given in <abnf.abnf>, and is based on [[RFC 5234]](https://datatracker.ietf.org/doc/html/rfc5234).
The differences are as follows:
* Numeric rules (prefixed by `%`) are only used in hexadecimal
* Bare (undelimited by `<>`) rulenames are not used.

## Lexical Grammar

The lexical grammar is described in <lex.abnf>, and describes the requirements for phase 2 translation.
 For the purposes of this grammar, ambiguous productions are resolved as follows:
1. First, tokens are resolved by building the largest possible valid lexical token with the input source characters,
 except that raw string literals are terminated at the first lexically valid terminator, and if a token matching the `dec-literal` production is followed immediately by characters that match the `..` or `..=` symbol, then the current token is lexed as a `dec-literal`, rather than a `float-literal`. 
2. Then, if a token matches the `bare-identifier` production, and the `keyword` production, then the token is a `keyword`
