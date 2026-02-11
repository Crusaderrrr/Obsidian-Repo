---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
  - browser
note type: Informational Note
---
# Stages 
1. **DOM**
2. **CSSOM**
3. **Render tree**
4. **Style calculation**
   - Applying the selectors to the elements
   - If selector is complicated the calculation will take more time
5. **Layout**
   - Browser knows what styles each element has
   - It creates a prototype of the page 
   - We get a *Layout tree*
6. **Paint**
   -  Browser paints the layout 
   - Creates a paint records 
7. **Compositing**
   - Work with layers 
   - Creates a *Layer tree*
   - Optimizes the layout for GPU 

When the button is clicked or another action executed that triggers re-render of the page, all the stages are getting involved from the beginning to the end.