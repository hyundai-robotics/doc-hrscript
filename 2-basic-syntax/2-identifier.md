# 2.2 Identifiers

Names must be given to commands, variables, functions, and labels that are described. These names are collectively referred to as “identifiers.” When deciding an identifier, it must comply with the following rules for the HRScript’s identifiers.

* It must consist only of uppercase and lowercase letters, numbers, and underscores.
* The first character must only be either a lowercase or uppercase letter or an underscore, not a number.
* It should not contain a space or tab.
* Identifiers already defined in the system, such as “if” and “for,” cannot be used.
* There is no limit to the length.

The following shows correct and incorrect examples of identifiers:

```text
myvar (O) 
myvar2 (O)
_myvar (O)
MyVar (O)
310a (X) – Started with a number
move (X) – An identifier already defined in the system
v300$ (X) – Used a symbol other than an underscore ($)
my var (X) – Included a space
```



