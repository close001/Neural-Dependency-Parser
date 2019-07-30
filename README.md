# Neural-Dependency-Parser
Dependency grammars posit relationships between "head" words and their modifiers, much like the function argument relations that are required by lexical entries in categorial grammar. These relationships consitute trees, in which each word depends on exactly one parent: either another word or, for the head of the entire sentence, a dummy root symbol, ROOT. This program implements a transition-based parser that incrementally builds up a parse one step at a time. At every step, the state of the (partial) parse is represented by:
- A stack of words that are currently being processed.
- A buffer of words yet to be processed.
- A list of dependencies predicted by the parser.

This is very much like a shift-reduce parser. Intially, the stack only contains ROOT, the dependencies lists is empty, and the buffer contains all words of the sentence in order. At each step, the parser advances by applying a "transition" to the partial parse until its buffer is empty and the stack is of size 1. The following transitions can be applied:
- SHIFT: removes the first word from the buffer and pushes it onto the stack
- LEFT-ARC: marks the second (second most recently added) item on the stack as a dependent of the first item and removes the second item from the stack.
- RIGHT-ARC: marks the first (most recently added) item on the stack as a dependent of the second item and removes the first item from the stack.

The parser uses a neural network as a classifier that decides which transition to apply at each state. 
