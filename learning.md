# learnings
1. Inspect scrolling - Enable show paint form rendering option, and see how
much paint is happening, if there's too much paint try to separate elements
on to layers( using will-change ), breaking down into separate layers makes
the browser only do compositing ( which is faster ), but too many layers
can also cause performance issues
2. requestAnimationFrame - If there's some visual change happening( something being added to the dom or elements animating on the page ), try to move
that particular code to requestAnimationFrame( instead of setTimeout or setInterval)
3. Forced synchronous layout - There are times when we are reading properties
like "offsetWidth", which requires layout calculation and on the basis of the 
read value, we update property which requires style calculation( ex style.left )
this trigger a read-write cycle, which causes forcedsynchronous layout.
inspecting with dev tools can tell you the function which is causing the issue.
Mostly refactoring the code or using css transforms instead of javascript
fixes the issue.
4. Javascript - Sometimes the javascript code itself is too time consuming, it makes sense to offload that work on to a web worker. Also, javascript code may be too slow or leaking memory, profiling JS is a good starting point in such scenario. ( remember everything must fit inside 10ms budget is we are animating)
5. Try to use the css properties which causes minimal execution in the pipeline
( Javascript -> Recalculate style -> Layout calculation -> Repaint -> Composite Layers)
6. Style recalculations can be reduced by using optimized selectors.
