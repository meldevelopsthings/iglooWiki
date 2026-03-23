For whatever reason, IGLOO makes you create your own script for all of this, so the technicians at Hallam helped by creating a script that does this. However we still need to set it up so here's how.

You only need one script to get this to work, and you can download it from the Google Drive link in the description of the tutorial video they sent out, called IglooPlayerInput.cs.

This then needs to be applied to the IglooManager object in Unity, don't worry about the World Canvas property, I haven't got that far yet.

Now for you to get this working, you will need to understand what the script is doing. *TL;DR is that it gets the main camera to shoot out a raycast from it's forward vector when either mouse left or gamepad south is pressed.*
![](/src/img/iglooPlayerInputScriptSnippet.png)

firePressed is just checking for a button input, this is where you can edit that.

cam just gets the **main** camera, and ensures it's not null. **MAKE SURE YOU HAVE NO MAIN CAMERAS IN YOUR SCENE, ONE SHOULD SPAWN DURING RUNTIME.**

The last line here basically just returns if a raycast that is shot out from the camera's forward vector results in a RaycastHit. This results in the "hit" variable, that is basically the **collider** you hit, not the object. To access this, and then the gameObject of this collider, simply use hit.collider.gameObject.

From here, you basically just need to have your main camera set up in such a way that; the centre of the camera can be moved via player input, and displays a crosshair for clarity. **There's a script for this and it's easy to setup if you know what to do.** 

Basically, head into Unity package manager and go to your project's igloo package. From here, just click the samples tab and select the player input system to import. As well as this, head into your project settings and click on the Player settings, in here open other settings and scroll until you find "Active Input Handling". **Set this value to both.**

Now you should have basic player input. By default, the south button on a game controller is what is used to "click".
