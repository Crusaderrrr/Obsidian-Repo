1. **Connection**
	Before any interaction happens, the connection is established via libpq and [[TCP-IP model|TCP]].
	After the raw SQL text is sent to the server (Postgres server)
2. **Parsing**
	- The string is tokenized (split into parts by keywords)
	- Parser checks the syntactical correctness and builds a parse tree (grammatical structure)
	- Semantic analyzer does w things:
		- looks up tables, functions, columns, everything that was referenced
		- Checks the user's permissions 
	- The grammatical tree is converted into SQL tree with references to real existing objects, not just words from query
3. **Rewriting**
	On that level the tree from step 2 is rewritten based on rules and views
4. **Planner / Optimizer**
	The most computationally intensive step
	Creates execution plan
	Generates paths 
	Decides on JOIN strategies 
	Cost estimation
5. **Execution**
	Walks through the plan tree from top to bottom
6. **Result return**
	Returns the result data in buffers or row by row depending on settings

<u>This is a very general structure, in reality it is much more complex.</u>
