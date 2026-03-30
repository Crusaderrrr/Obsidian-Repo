
1. **Names Should Reveal Intent**
	- A name must answer: *why* it exists, *what* it does, and *how* it is used
	- If a name requires a comment — it fails to reveal intent
	- Bad: `int d; // elapsed time` → Good: `int elapsedTimeInDays`

2. **Avoid Disinformation**
	- Don't use names with hidden meanings (`hp`, `aix`, `sco` are associated with Unix platforms)
	- Don't name a group `accountList` unless it actually is a `List` — use `accounts` or `accountGroup`
	- Avoid names that look nearly identical (e.g. `XYZControllerForEfficientHandlingOfStrings` vs `XYZControllerForEfficientStorageOfStrings`)
	- Never use lowercase `l` or uppercase `O` next to digits `1` and `0`

3. **Make Meaningful Distinctions**
	- Number-series names (`a1, a2`) carry no meaning — prefer `source, destination`
	- Noise words like `Info`, `Data`, `Object` don't create real distinctions
	- Words like `variable`, `table`, `data` are redundant in names
	- `getActiveAccount()`, `getActiveAccounts()`, `getActiveAccountInfo()` — a reader can't tell which to call

4. **Use Pronounceable Names**
	- If a name can't be pronounced aloud — it's a bad name
	- Bad: `genymdhms` → Good: `generationTimestamp`
	- Programming is a social activity; names must work in conversation

5. **Use Searchable Names**
	- Single-letter names and numeric constants are hard to find in a large codebase
	- Bad: `7`, `e` → Good: `MAX_CLASSES_PER_STUDENT`
	- Single-letter names are acceptable **only** for local variables in short methods
	- The length of a name should correspond to the size of its scope

6. **Avoid Encoding Schemes**
	- **Hungarian Notation** (`strName`, `iCount`) is obsolete — modern IDEs and compilers track types
	- **`m_` prefix** for class members is unnecessary — IDEs highlight fields visually
	- Encoding types into names makes code harder to read, refactor, and understand


## Conclusion

We *read the code*, as the author the most important thing is to deliver the information *the clearer the better*, we want the other person to *understand what the code does at the first glance*.