1. **POLA** (POLS)
	which stands for principle of least astonishment, or principle of least surprise, and it is a design rule. *The function should do what the user expects it to do*.
2. **Edge cases**
	every edge case should be covered with test
3. **Duplication - bad**
	All the [[OOP]] principles are dedicated to remove duplication
	many patterns are also done for that
	etc.
4. **Base classes**
	 A base class should not be depending on a derived class.
5. **Too much information**
	Focus on making simple interfaces, simple functions, simple classes
	Do not overcomplicate
6. **Dead code**
	If you see any dead code (`switch/case`, `if/else`, small helper method that will never be used), do the right thing - get rid of it.
7. **Vertical division**
	You should read the code as a newspaper (from top to bottom)
	private methods should be declared right after the first caller method (conventionally)
8. **Esequence**
	E.g. if you used a name `response` for managing `HttpServletResponse`,  be consequent, use this same name in other methods to work with `HttpServletResponse`. That can be propagated to any concept, not only variables.
9. **Time management**
	If you want to put some code anywhere, firstly check if this is the appropriate place for this exact code (could be constant variable or smt), because generally if you are lazy ass and put it without investigating, that would cause problems later.
10. **Do not use** [[Magic numbers]], use `CONSTANTS` instead

**Interesting one**:
- If you do not understand how function works, divide it into pieces that small, that it is obvious what this piece does.