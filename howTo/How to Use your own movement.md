when using the player controller youll have to chek the Igloo Manager incase of the main camera causing issues.

<img width="316" height="203" alt="image" src="https://github.com/user-attachments/assets/8f3df603-e136-4661-834e-e004a3e53605" />

When the Igloo Manager is added it will look for a camera named Main Camera and attach itself to it. This causes issues as it can stop the camera that the Igloo Manager spawns to either not be able to move and be stuck in place or focus/look in the same direction as it. So, when adding the Igloo manager you should check to see if the Main Camera has been attached to it and unattach it, or if it is unattached but the issue is still there then removing the Main Camera should work.

