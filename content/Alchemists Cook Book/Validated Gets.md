
Validated Gets are a means of **removing a step** when ensuring that no *false returns* are generated from **empty variables** and even better - they grant a concise means of delivering instructions and context events to the **presence** or **non-presence** of a *variable*!

![[IO_TraceCode.png]]
This is the **Interaction trace** that scans for *Interactive Objects* as part of the [[HANGER]]! This check simply does two validation checks based on if the player trace **is colliding** or **is not colliding** with an *interactive object*!

If it **is colliding** then it checks if it was *previously colliding* with a different object, if **valid** then it will *switch off it's interact Widget* using the *saved object ref* and then setting the new *Saved Object Ref* as the **currently traced** **Interactive Object!** 

If the trace is *colliding with nothing* then it checks if it was previously looking at something and to use the previous *Saved Object Ref* to switch off it's widget and **then clear that Ref** so it is not needlessly re-calling that event! Once cleared, the failed trace does *nothing*.