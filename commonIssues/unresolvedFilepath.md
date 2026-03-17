This issue occurs when trying to pull from a repo that has the IGLOO Unity project setup incorrectly. This happens because of how the package is installed and how the Unity package manager handles that; it basically just throws an error because it's trying to find the files for the package where it won't find them.

This is because the package manager looks at ~/Packages/manifest.json to find where the actual file is to install the IGLOO package. By default, Unity will point to where the file is stored on the host's computer, so if you look at what filepath the package manager is trying to look for, it will actually just be something like "Packages/home/user/Downloads/". **This is obviously wrong and we should fix it.**

Thankfully this is a simple process where you simply:
- Open your project's manifest.json file (Typically in ~/Packages/).
- Look for the "com.igloo.toolkit" line with a filepath.
- Create a folder somewhere in your project and store the IGLOO package there.
- Change the manifest.json filepath to be that filepath you just created.
- Test and it should work.

Here's an example of what you should have:
![](/src/img/correctedFilePath.png)
