


### :luc_locate_fixed: Does Implement Interface

Can be used in **Trace** or *Overlap* styled events to query if the *Queried Actor* contains a specific *Interface* and return a **Boolean** answer - This was ESPECIALLY useful during the [[HANGER#luc_person_standing Player Character | Hanger Character]] *sphere trace* that checks only for *interactive objects*!

Using **Does Implement Interface** meant that the *Sphere Trace* could **ignore** *non-interactive objects* - Fixing that problem that caused the *Sphere Trace* to be blocked by *Regular Static Mesh's* such as Tables that the actual **Interactive Object** was sitting on top of!


![[DII_Img.png]]![[Pasted image 20241206142059.png]]![[Pasted image 20241206142112.png]]