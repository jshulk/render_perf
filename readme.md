# Rendering performance notes
* 16ms to render a single frame, which is actually ~10ms, given that 
  browser also does some house keeping stuff.

## Phases of rendering
* Parsed HTML
* PARSED HTML + CSS ( [Recalculate style] ) => Render Tree ( only the visible elements form the render tree)
* Once the browser knows what elements it has to display, it starts
doing the layout( calculates the position and dimensions of the elements)
At this point the render tree actually turns into a collection of boxes. [layout]
* [ Reflow ] is same as [ Layout ]
* Vector to Raster
  1. Initially all the elements are vectors they are rasterized on to pixels
  2. [ Paint ] steps ( example )
    * drawRectangle
    * drawText
    * drawBitmap
    * translate
    * restore
  3. [ Composite ] layers - ( putting multiple layers together)
  4. Layers and tiles are uploaded to GPU 
* [ Layout ] - Layout scope is usually the whole document

## Pipeline
### Javascript >> Style >> Layout >> Paint >> Composite ###
* Flow 1
   1. Javascript/css based animation made some visual change
   2. Browser recalculates the style of all the affected elements.
   3. If the visual change made any difference in dimension/position
	of an element, this would trigger a reflow of the document.
   4. Any affected areas will need to be repainted
   5. Finally the painted elements need to be composited together.
* Flow 2
  1. Change a paint only property like background image, text color, shadows etc ( with js or css)
  2. Browser recalculates styles.
  3. We don't do layouts, because we didn't change geometry of the elements
  4. Paint
  5. Composite

* Flow 3
  1. Change so that only compositing is required( no paint or layout )
  2. browser recalculates
  3. No layouts
  4. No paint
  5. Composite
