When trying to use Unity's canvasses on the IGLOO screen, they likely won't show up there, but they will inside of the editor and on flatscreen devices. This is due to the default value assigned to the canvas property "Render Mode", which should be set to Screen Space - Overlay by default. 

To fix this is really simple, just change this property to Render Mode: World Space.
This will place your canvas into the Unity environment and will allow you to resize and move it just like any Unity GameObject. In order for it to function correctly with the Igloo Player Input system, **every interactable element in the UI should have a Box Collider component added to it**.

### Alternative Fix

An alternate fix is to spawn 2d objects in the 3d space and use that as UI. Right click the left panel > 2D objects > sprites.

For example, in the project we had dialogue boxes appear next to the NPC's head and cycle through dialogue in space.
