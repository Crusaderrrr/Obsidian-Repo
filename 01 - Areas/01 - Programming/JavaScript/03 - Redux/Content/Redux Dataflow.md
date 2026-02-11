---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
  - redux
note type: Informational Note
---
Redux keeps your app’s data moving in a straight, easy-to-follow path called **unidirectional data flow**. This means data travels one way, like a one-way street, which helps when your app gets big and complicated. Without this control, it’s hard to fix problems or add new stuff. Redux makes it simpler by setting clear rules for updating data.

Here’s how it works, step by step, using the diagram:

1. **View (Your App’s Screen)**
    - This is what users see (like a button or list). When they click something (an "event"), it starts the process.
2. **Actions (The Instructions)**
    - When a user does something (like clicking "Add Task"), an Action is created. It’s a simple note, like { type: "ADD_TODO", task: "Buy milk" }, telling Redux what to do.
3. **Dispatcher (The Messenger)**
    - The Dispatcher takes the Action and sends it to the Store. Think of it as a delivery person carrying the note.
4. **Store (The Data Hub)**
    - The Store is like a big box that holds all your app’s data (the "State"). Inside the Store, the Reducer looks at the Action.
5. **Reducer (The Decision Maker)**
    - The Reducer is like a rule-following assistant. It takes the current data (State) and the Action, then decides the new data. For example, if the Action is "ADD_TODO," it adds the new task to the list. It might split the work into smaller helpers but always gives back an updated State.
6. **State (The Updated Data)**
    - This is the new data after the Reducer does its job, like { todos: ["Buy milk"] }. The Store updates with this.
7. **Back to View**
    - The Store tells the View, “Hey, the data changed!” The View then grabs the new State and updates the screen (re-renders) so users see the change (like the new task appearing).

A scheme:
![[Pasted image 20250513122046.png]]
