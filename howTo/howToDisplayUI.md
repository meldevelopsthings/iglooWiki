UI doesn't display by default because of how IGLOO functions (I don't know). Simply put: the IglooManager is supposed to spawn a main camera that is used to display a UI canvas, but it doesn't. Instead, we need to manually sort it.

The main thing is to create a main camera object, and then set your canvas Render Mode property to "Screen Space - Camera" and set the Render Camera to the main camera object.

This is what it should look like:

![](/src/img/canvasCorrection.png)

You'll see that the canvas is no longer huge in the editor; this represents the actual size of the UI and shows it in the game environment, as that's what this does effectively. Because of this, you should probably consider how that will affect your UI and interaction.
