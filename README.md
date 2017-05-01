# NP_station

Blender np_station extension for external addon access proposal

Access from outside in your own modal operators:


```
from np_station.np_point_move import snap_point

in your modal invoke()
    sp = snap_point()    
    sp.invoke()
    or
    sp.invoke(takeloc=Vector(your predefined takeloc))
    then add your handler
    
in your modal modal()
    
    sp = snap_point()
    if sp.is_running:
        .. whatever you want to do while running
        return {'RUNNING_MODAL'}
    if sp.is_success:
        .. whatever you want to do
        return {'FINISHED'}
    if sp.is_cancel:
        return {'CANCELLED'}
    
    you may use 
    
    sp.delta    Vector delta from start and end point
    sp.takeloc  Vector start location
    sp.placeloc   Vector end location

```
