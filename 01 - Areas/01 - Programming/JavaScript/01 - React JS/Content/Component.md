---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - React_JS
  - JavaScript
  - programming
note type: Informational Note
---
**UI** (User Interface) part of React consists of **Components**
- those are JS functions that have JSX text inside and return it, not HTML
- need to be defined 

*Example*
```JavaScript
export default funtion funcName () {
return (
	<p>Poshel nahuy</p>
	);
}
```

**funcName** always needs to start with a CAPITAL letter 
- Can't define one component inside another 

*Example of nested component* (Profile is nested)
```JavaScript
function Profile() {
  return (
    <img
      src="https://i.imgur.com/MK3eW3As.jpg"
      alt="Katherine Johnson"
    />
  );
}

export default function Gallery() {
  return (
    <section>
      <h1>Amazing scientists</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}

```

class -> className

To return more than one element as JSX:
```JavaScript
function App() {
	<> // empty component (React Fragment)
		<Header />
		<Main />
	</>
};
```

Also, we can use curly braces `{}` inside those elements to link to other elements, defined in variables:
```JavaScript
const src = "https://i.imgur.com/MK3eW3As.jpg"
function Profile() {
  return (
    <img
      src={src} // this 
      alt="Katherine Johnson"
    />
  );
}
```