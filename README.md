# CYK Algorithm

## A Java implementation of the CYK-Algorithm.

The CYK-Algorithm can be used to check if a word can be derived from a CFG (context-sensitive grammar).

You only need you grammar to be in the CNF (Chomsky normal form) format. This Java application will parse an external grammar file and then output the result visualized in a table.

## Grammar File

A grammar file will have the following structure.

```
S                             -> Starting Symbol
a b                           -> Terminals
S A B E C X Y Z               -> Non-Terminals
S YB XA *                     -> 4th and all following lines are production rules
E YB XA                       -> You can add multiple to one terminal if you seperate them by a space
A a YE XC                     -> This reads as A -> a | YE | XC
B b XE YZ
C AA
X b
Y a
Z BB
```

After you compiled the .java file you can simply run it via

```
java CYK <GrammarFile> <Word>
```

Sample output for the supplied grammar above:

```
$ java CYK grammar.txt abbbabaa
Word: abbbabaa

G = ({a, b}, {S, A, B, E, C, X, Y, Z}, P, S)

With Productions P as:
A -> a | YE | XC
B -> b | XE | YZ
C -> AA
E -> YB | XA
S -> YB | XA | *
X -> b
Y -> a
Z -> BB

Applying CYK-Algorithm:

+-------+-------+-------+-------+-------+-------+-------+-------+
| a     | b     | b     | b     | a     | b     | a     | a     |
+-------+-------+-------+-------+-------+-------+-------+-------+
| A,Y   | B,X   | B,X   | B,X   | A,Y   | B,X   | A,Y   | A,Y   |
+-------+-------+-------+-------+-------+-------+-------+-------+
| E,S   | Z     | Z     | E,S   | E,S   | E,S   | C     |
+-------+-------+-------+-------+-------+-------+-------+
| B     | -     | B     | B     | A     | A     |
+-------+-------+-------+-------+-------+-------+
| Z     | Z     | Z     | E,S   | C     |
+-------+-------+-------+-------+-------+
| B     | -     | B     | A     |
+-------+-------+-------+-------+
| Z     | Z     | E,S   |
+-------+-------+-------+
| B     | B     |
+-------+-------+
| E,S   |
+-------+

The word abbbabaa is an element of the CFG G and can be derived from it.
```
