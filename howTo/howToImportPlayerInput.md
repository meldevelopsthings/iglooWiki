With the initial setup, input won't work, so here's how to set it up. 

First, head over to the package manager, and click on the igloo package. From here, you should see one tab labelled as "Samples"; click on this and select import for player system.

![](src/img/playerInputInPackages.png)

As well as this, because this player system uses Unity's legacy input handling, you also need to change the **active input handling to be both.** You can do this by heading to project settings, heading to the player tab, and scrolling until you find this field; or you can search for it. Below is the default, that needs to be updated:

![](src/img/changeActiveInputHandling.png)

This will get you the majority of the way there, creating a cursor that can be manipulated with mouse and game controller, as well as allowing for smooth movement with WASD or control stick.

This doesn't, however, allow for **clicking with the cursor; there's no handling for it anywhere.** For whatever reason, IGLOO makes you create your own script for this bit, so the technicians at Hallam helped by creating a script that does this, as they had discovered these issues before us. Info about this script is at the end of this doc.

# So how do we set up clicking?
Well, we just need a script to find the main camera in the current scene. Thankfully, Unity has an easily accessible member for this; Camera.main. Simply use this line of code to reference the main camera, which is being used to manage the crosshair through the rotation of the main camera.

But then what? Well, now we can fire out a [raycast](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Physics.Raycast.html) from the main camera, which basically just translates to; if this main camera is able to look at and see a collider component, that collider is then returned as a "hit". Because of the main camera representing the cursor, this should hopefully explain how and why the igloo checks to see if the cursor is clicking on something.

This is probably along the lines of the code you'll want:
```
// Only do this on a mouse click, or game controller button press.
if (Mouse.current.leftButton.wasPressedThisFrame || Gamepad.current != null && Gamepad.current.buttonSouth.wasPressedThisFrame) 
{
	Camera cam = Camera.main;
	
	// Shoot the raycast from the centre of the camera.
	if (!Physics.Racast(cam.transform.position, cam.transform.forward, out RaycastHit hit)) return;
	
	// See the tag of the clicked object, and see if it is a clickable object.
	switch (hit.collider.gameObject.tag)
	{
		case "YourObjectTag":
			// On click logic here!
		break;
	}
}
```

This should allow you to handle clicking properly in your project.
# IOT Script
You only need one script to get this to work, and you can download it from the Google Drive link in the description of the tutorial video they sent out, called IglooPlayerInput.cs.

This then needs to be applied to the IglooManager object in Unity, don't worry about the World Canvas property, I haven't got that far yet.

Now for you to get this working, you will need to understand what the script is doing. *TL;DR is that it gets the main camera to shoot out a raycast from it's forward vector when either mouse left or gamepad south is pressed.*
![](/src/img/iglooPlayerInputScriptSnippet.png)

firePressed is just checking for a button input, this is where you can edit that.

cam just gets the **main** camera, and ensures it's not null. **MAKE SURE YOU HAVE NO MAIN CAMERAS IN YOUR SCENE, ONE SHOULD SPAWN DURING RUNTIME.**

The last line here basically just returns if a raycast that is shot out from the camera's forward vector results in a RaycastHit. This results in the "hit" variable, that is basically the **collider** you hit, not the object. To access this, and then the gameObject of this collider, simply use hit.collider.gameObject.
