# DSL for Block Diagram Specification

In this page, we give examples of the layout & the corresponding DSL syntax.

We specify the grammar for the DSL which has to be parsed.

## Layering of 2 or 3 Blocks

```
+---+---+     
|   A   |     
+---+---+   +-A-----+  
|   B   |   | +---+ |  
+---+---+   + | B | +  +---+---+---+
|   C   |   | +---+ |  | A | B | C |
+-------+   +-------+  +---+---+---+
:A,B,C:       A > B    |A,B,C|
```

Two blocks 2 layers variations:

```
+---+---+   +---+---+   +---+---+   +---+---+
| B |   |   |   | B |   | A     |   |     A |
+---+   |   +   +---+   +   +---+   +---+   +
|     A |   | A     |   |   | B |   | B |   |
+-------+   +-------+   +-------+   +-------+
!A,B!       %A,B%       $A,B$       #A,B#
```

## Two Layers Variations using 3 Blocks

```
+---+---+      +---+---+    +---+---+     +---+---+ 
| A | B |      |   A   |    | A |   |     |   | B | 
+---+---+      +---+---+    +---+ C +     + A +---+ 
|   C   |      | B | C |    | B |   |     |   | C | 
+-------+      +-------+    +-------+     +-------+ 

:|A,B|, C:     :A,|B,C|:    |:A,B:,C|     |A,:B,C:|

```

Few more 2 layer 3 blocks variations:

```
+---+---+--+   +---+---+--+   +---+---+--+   +---+---+--+  
| A | B |  |   | A        |   |   | B |C |   |        A |  
+---+---+  |   +   +---+--+   +   +---+--+   +---+---+  |  
|     C    |   |   | B |C |   | A        |   | B | C |  |  
+-------+--+   +-------+--+   +-------+--+   +-------+--+  
!|A,B|,C!      $A,|B,C|$      %|B,C|,A%      #|B,C|,A#     

```

### Three Layers - Variations

```
+---+---+      +---+---+    +---+---+   +---+---+  
| A |   |      |   C   |    | A     |   |   | A |  
+---+   +      +---+   +    +   +---+   +   +---+  
| B |   |      | A |   |    |   | A |   |   | B |  
+---+   +      +---+   +    +   +---+   +   +---+  
|     C |      | B |   |    |   | B |   | C     |  
+-------+      +-------+    +-------+   +-------+  
!:A,B:,C!      #:A,B:,C#    $:A,B:,C$   %:A,B:,C%

```

A few more weird variations of 3 blocks in 3 layers:

```
+---+---+    +---+---+   +---+---+   +---+---+   
|   A   |    |   | C |   | C |   |   |   A   |  
+---+   +    +   +---+   +---+   +   +   +---+  
| C |   |    | A     |   |     A |   |   | C |  
+---+---+    +---+---+   +---+---+   +---+---+  
|   B   |    |   B   |   |   B   |   |   B   |  
+-------+    +-------+   +-------+   +-------+  
:#A,C#,B:    :%A,C%,B:   :!A,C!,B:   :$A,C$,B:  

+---+---+    +---+---+   +---+---+   +---+---+ 
|   B   |    |   B   |   |   B   |   |   B   | 
+---+---+    +---+---+   +---+---+   +---+---+ 
|       |    |     A |   | C |   |   |   | C | 
+ A +---+    +---+   +   +---+   +   +   +---+ 
|   | C |    | C |   |   |     A |   | A     | 
+-------+    +-------+   +-------+   +-------+ 
:B,$A,C$:    :B,#A,C#:   :B,!A,C!:   :B,%A,C%:

+---+---+   +---+---+  +---+---+  +---+---+ 
|   | C |   |   | C |  | A     |  | C |   | 
+ B +---+   +   +---+  +   +---+  +---+ B + 
|   |   |   |   |   |  |   |   |  |   |   | 
+---+   +   +   + B +  +---+ B +  +   +---+ 
|     A |   | A |   |  | C |   |  | A     | 
+-------+   +-------+  +-------+  +-------+ 
  ??        |A,:C,B:|  $A:C|B     C:%A|B
```

Some nice block with sub-block diagram variations:

```
+---+---+---+    +---+---+---+   +---+---+---+  
|   |   A   |    |   |   | B |   |         C |  
+   +---+   +    +   +   +---+   +---+---+   +  
|   | B |   |    |   | A     |   |   | B |   |  
|   +---+---+    |   +---+---+   |   +---+   +  
| C         |    | C         |   | A     |   |  
+-----------+    +-----------+   +-----------+  
%C,#A,B#%a       %C,%A,B%%        #C,%A,B%#

```

A few more weird variations of 3 blocks in 3 layers:

```
+---+---+---+   +---+---+---+   +---+---+---+   +---+---+---+ 
|   A       |   | A     |   |   |   |     A |   | A         | 
+---+---+   +   +   +---+   +   +   +---+   +   +   +---+---+ 
|   | B |   |   |   | B |   |   |   | B |   |   |   | B |   | 
|   +---+---+   |   +---+   +   |   +---+   +   +---+---+   + 
| C         |   |   |     C |   | C     |   |   |         C |
+-----------+   +-----------+   +-----------+   +-----------+
???                   ???          %C|#A|B             ???
```

## Grammar of the Specification

PEG.js grammar to be included once we fix the syntax notation.

```
blk_diag = node_mod? node_name (op blk_diag)*
op = [\:\|>]
node_mod = [%$#!]
node_name = [A-Za-z]
```

## AST Output - Example Inputs

Given below are some of the expected AST outputs for sample input expressions:

|A,:C,B:| - expected AST is:

```
{"pipe": ["A", "colon": ["C","B"]]}
```
