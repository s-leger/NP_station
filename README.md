# NP_station

Blender np_station extension for external addon access proposal

Access from outside in your own modal operators:


```
from np_station.np_point_move import snap_point

in your modal invoke()
    sp = snap_point()    
    
    sp.invoke()
    sp.invoke takes 2 optinnal arguments:
    
    takeloc : Vector define your start location so the 
        tool use it and begin in place mode
        
    callback: function(context, event, state): 
        a function to call back when tool change state
        witch take context, event and state in {'RUNNING', 'SUCCESS', 'CANCEL'}
        as arguments
        
    sp.invoke(takeloc=Vector(your predefined takeloc), callback=your_callback)
    
    then add your handler
    
in your callback():
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
    
    
NOTE: 
    mouse move events are captured by np_snap operator,
    so if you want update while the tool is running
    you'll have to use a TIMER based event.
    
    then in your modal modal()
    if event.type == 'TIMER':
        sp = snap_point()
        .. do whatever you want at update time

```
