# Cannon Grammars

This folder describes the grammars used by the Cannon Language, written in a subset of ABNF. 

The syntax of the grammar specifications is given in <abnf.abnf>, and is based on [[RFC 5234]](https://datatracker.ietf.org/doc/html/rfc5234).
The differences are as follows:
* Numeric rules (prefixed by `%`) are only used in hexadecimal
* Bare (undelimited by `<>`) rulenames are not used.
* Whitespace between parts of a rule are ignored.

## Lexical Grammar

The lexical grammar is described in <lex.abnf>, and describes the requirements for phase 2 translation. The lexical grammar is whitespace sensitive, any whitespace in a production that is not matched by any rule is not allowed.
 For the purposes of this grammar, ambiguous productions are resolved as follows:
1. First, tokens are resolved by building the largest possible valid lexical token with the input source characters,
 except that raw string literals are terminated at the first lexically valid terminator, and if a token matching the `dec-literal` production is followed immediately by characters that match the `..` or `..=` symbol, then the current token is lexed as a `dec-literal`, rather than a `float-literal`. 
2. Then, if a token matches the `bare-identifier` production, and the `keyword` production, then the token is a `keyword`

The following non-terminals defined in prose are included as non-terminals in <lex.abnf>:
* `XID_Start`, which is any unicode character with the property `XID_Start` as defined by UAX #31 from Unicode 15.0.
* `XID_Part`, which is any unicode character with the property `XID_Part` as defined by UAX #31 from Unicode 15.0.

## Syntactic Grammar

The Syntactic Grammar is described in <ast.abnf>, and describes the requirements for phase 3-5 translation. The syntactic grammar is whitespace insensitive. Whitespace is allowed between terminals and non-terminals, but whitespace is not allowed within terminal productions. The productions defined in <lex.abnf> are included as non-terminals in <ast.abnf>.