# Strict mode of javascript

An ECMAScript Script syntactic unit may be processed using either unrestricted or strict mode syntax and semantics. Code is interpreted as strict mode code in the following situations:

Global code is strict mode code if it begins with a Directive Prologue that contains a Use Strict Directive \(see 14.1.1\).

Module code is always strict mode code.

All parts of a ClassDeclaration or a ClassExpression are strict mode code.

Eval code is strict mode code if it begins with a Directive Prologue that contains a Use Strict Directive or if the call to eval is a direct eval \(see 12.3.4.1\) that is contained in strict mode code.

Function code is strict mode code if the associated FunctionDeclaration, FunctionExpression, GeneratorDeclaration, GeneratorExpression, MethodDefinition, or ArrowFunction is contained in strict mode code or if the code that produces the value of the function’s \[\[ECMAScriptCode\]\] internal slot begins with a Directive Prologue that contains a Use Strict Directive.

Function code that is supplied as the arguments to the built-in Function and Generator constructors is strict mode code if the last argument is a String that when processed is a FunctionBody that begins with a Directive Prologue that contains a Use Strict Directive.

ECMAScript code that is not strict mode code is called non-strict code.

