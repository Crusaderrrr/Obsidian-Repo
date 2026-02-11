---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - event_loop
  - JavaScript
note type: Informational Note
---
```javascript
// create a new observer instance
const mutationObserver = new MutationObserver( (mutations) => {
	console.log(mutations);
})

// things we want to observer
mutationObserver.observe(header, { 
	subtree: true,
	attributesOldValue: true,
	childList: true
})
```

- In a few words, this is a special mechanism that allows us to observer all [[DOM]] changes.
- The code above will log the elements that was changed.
- That object generates *Microtasks*. 