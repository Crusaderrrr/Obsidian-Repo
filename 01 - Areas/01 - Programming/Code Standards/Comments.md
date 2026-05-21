These are some general rules for commenting code.

1. **Only technical information** (code/architecture)
	This means that all the info that is like metadata (author name, last modified date, etc.), other information that is generally handled by other protocols or tools (e.g. git) should not be present in comments.
2. **Obsolete comment**
	Many comments become obsolete very quickly, they also can become a source of lie. They should either be update or removed.
3. **Excessive comment**
	Excessive comment is a comment that tells you something obvious:
	`i++; // Inceremtns variable i`
	a javadoc comment could also tell you more then needed, or less, in case if it just a function signature 
4. **General rules**
	- Be concise
	- No grammatical/punctuational errors 
	- Do not tell obvious info
	- The comment should be clear
5. **Commented out code**
	Worst thing that can happen
	Best thing that can be done - removing it