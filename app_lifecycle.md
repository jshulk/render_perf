# Application Lifecycle

# RAIL
R - Response
A - Animation
I - Idle
L - Load

Load - load the critical piece of functionality ( Time - 1s )
Idle - Load images, videos, comments ( Time - 50ms( chunks ) )
Response - Need to respond to user input ( Time - 100ms )
Animation - (Time - 16 ms)

## Animations
F - first ( initial state of the element) 
L - last ( last state of the element )
I - Invert ( run the animation in reverse)
P - Play ( run the animation)

FLIP basically allows us to pre compute the calculations required
to do the animation 
Entire FLIP should be completed in Response(RAIL) time ( 100ms )

Example
1. Collect properties of card in collapsed position
2. Expand the card and collect the properties again.
3. Figure out differences and transform the card back
4. Wait for a frame( requestAnimationFrame ) trigger the animation and remove
invert transform and opacity changes.
5. if an opacity or transform changes affects element on its own layer, paint won't need to be run.
6. clip - used to reverse animation ( triggers paint )

LOAD - load ev
