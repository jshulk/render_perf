# Rendering performance notes
* 16ms to render a single frame, which is actually ~10ms, given that 
  browser also does some house keeping stuff.

## Phases of rendering
* Parsed HTML
* PARSED HTML + CSS ( Recalculate style ) => Render Tree