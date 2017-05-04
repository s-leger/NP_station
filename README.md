# NP_station

Blender np_station extension for external addon access proposal

Access from outside in your own modal operators:


```
from np_station.np_point_move import snap_point

in your modal invoke()
    sp = snap_point()    
    
    sp.invoke()
    sp.invoke takes 5 optionnal arguments:

    callback: optionnal function(context, event, state in {'RUNNING', 'SUCCESS', 'CANCEL'}) 
              called on state changes
    draw_callback: optionnal function(context) 
                   allow to add our own defined draw function updated while running
    takeloc : optionnal start in PLACE mode using this point as takeloc
    constrain: when true, constrain placeloc over a plane defined by takeloc and normal
               snap over apparent location of point projected to plane.
    normal: normal of constrain plane default to Vector((0,0,1)) for 2d plane XY
            fallback to view normal on ortho viewport
        
    sp.invoke(takeloc=Vector(), callback=your_callback, draw_callback=your_draw, constrain=True, normal=Vector((0,0,1)))
    
    then add your handler
    
in your callback(context, event, state):
    sp = snap_point()
    
    if state == 'RUNNING':
        .. whatever on take loc    
    elif state == 'SUCCESS':
        .. whatever on place success
    elif state == 'CANCEL'
        .. whatever when user cancel
        
    you may use:
    sp.delta    Vector delta from start and end point
    sp.takeloc  Vector start location
    sp.placeloc   Vector end location


in your modal modal()
    
    sp = snap_point()
    you may use 
    sp.delta    Vector delta from start and end point
    sp.takeloc  Vector start location
    sp.placeloc   Vector end location
    
    


```
