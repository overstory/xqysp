XQYSP
===

Yet another parser?
---

Recently I needed to parse a fairly sophisticated search syntax for a project.
I needed a pure XQuery solution, and MarkLogic's built-in search API
wouldn't handle some of the syntax: nested groups, for example.
So I wrote another one.

Here is a rough cut at the BNF

    L ::= expr*
    expr ::= group | infixExpr | term
    group ::= prefixOp? '(' expr* ')'
    prefixOp ::= "+" | "-" | "~" | "NOT"
    infixExpr ::= (term | group) " " infixOp " " (term | group)
    infixOp ::= "*" | "OR" | "|" | "AND"
    term ::= prefixOp? (field fieldOp)? (group | literal)
    field ::= (letter | "_")+
    fieldOp ::= [":" | "=" | ">" | ">=" | "<" | "<="]
    literal ::= word | quoted_words
    quoted_words ::= '"' word (" " word)* '"'
    word ::= (letter | digit | "_")+
    number ::= digit+
    letter ::= [A-Za-z]
    digit ::= [0-9]

This could make a nice template for your own search parser,
or patches are welcome.

The test cases use [XQUT](https://github.com/mblakele/xqut).
If you find problems, please provide a test case.

License
---
Copyright (c) 2011 Michael Blakeley. All Rights Reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

The use of the Apache License does not indicate that this project is
affiliated with the Apache Software Foundation.