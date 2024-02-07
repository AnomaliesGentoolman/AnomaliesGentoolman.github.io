---
layout: post
title: Compiled TModloader and Terraria with Goldberg Emulator
---

Yeah this is right, i compiled terraria and tmodloader with Goldberg Steam Emulator (which is open-source) and now the game is actually pirated now.


I just have terraria legally, i was bought it from steam but i was just curious about can i compile the tmodloader and terraria source code with goldberg?
And yeah it worked i will cover how did i did it in this post.

---


I just installed the Terraria from steam and just get the TModloader source code from github, i needed to fork the TModloader repository before cloning.


I did ``git clone https://github.com/WH0LEWHALE/tModLoader`` and cloned the repository.


Then i installed .NET 6.0 SDK and XNA Framework 4.0 in the Terraria game directory in order to compile and run the TModloader.


The fact that TModloader has Terraria source code in it, it was awesome.


Okay so, when i cloned the repository i launched **setup.bat**.


A Terminal popped up and installed some dependencies well hey there we go!


<img src="../images/terraria-post/Annotation%202024-02-07%20131135.png" width="420" height="400">


Now then i just clicked **Setup** button and its Done.


We have terraria and tmodloader source code right now, I just clicked **"TModloader.sln"** from **``tModLoader\solutions``** (You can enter **Terraria.sln** or other one too but i just wanted terraria with tmodloader).


And boom here we have a full source code and even i can run it,

![mega-archive](../images/terraria-post/Annotation%202024-02-07%20132240.png)

But there is a problem and thats our topic, i need to open steam in order to run the tmodloader, but what if i put Goldberg Steam Emulator .dll's? does it work?


Yeah it works but its a bit hard but i will explain with the easiest way.

You need change some .dll's from the game and source code directory.


Get the goldberg emulator .dll's from here: https://github.com/WH0LEWHALE/goldberg-emu/releases/tag/release


or you can get from the original repository: https://gitlab.com/Mr_Goldberg/goldberg_emulator/


And then i just did these steps in order to implement the Goldberg Steam Emulator,
(you can just change the name of the original steam_api.dll to steam_api_orig.dll for backup)

Replace the steam_api.dll in the ``"\Steam\steamapps\common\Terraria"`` directory.

Replace the steam_api.dll in the source code ``\tModLoader\ExampleMod\bin\Release\net6.0\Libraries\Native\Windows`` directory.

Replace the steam_api.dll in the source code ``\tModLoader\src\tModLoader\Terraria\bin\Release\net6.0\Libraries\Native\Windows`` directory.

Replace the steam_api.dll in the source code ``\tModLoader\src\tModLoader\Terraria\Libraries\Native\Windows`` directory.

Replace the steam_api.dll in the source code ``\tModLoader\test\bin\Release\net6.0\Libraries\Native\Windows`` directory.

Replace the steam_api.dll in the source code ``\tModLoader\src\TerrariaNetCore\Terraria\Libraries\Native\Windows`` directory.

Replace the steam_api.dll in the source code ``\tModLoader\patches\TerrariaNetCore\Terraria\Libraries\Native\Windows`` directory.

And now you need to add some // to some code lines,

**InstallVerifier.cs, Line 198**

```
if (!HashMatchesFile(steamAPIPath, steamAPIHash)) {
	 Utils.OpenToURL("https://terraria.org");
	ErrorReporting.FatalExit(Language.GetTextValue("tModLoader.SteamAPIHashMismatch"));
	return;
}
```

to


```
if (!HashMatchesFile(steamAPIPath, steamAPIHash)) {
	// Utils.OpenToURL("https://terraria.org");
	// ErrorReporting.FatalExit(Language.GetTextValue("tModLoader.SteamAPIHashMismatch"));
	return;
}
```

**InstallVerifier.cs, Line 223**

```
case TerrariaSteamClient.LaunchResult.ErrInstallOutOfDate:
	ErrorReporting.FatalExit(Language.GetTextValue("tModLoader.TerrariaOutOfDateMessage"));
	break;
```

to


```
case TerrariaSteamClient.LaunchResult.ErrInstallOutOfDate:
//	ErrorReporting.FatalExit(Language.GetTextValue("tModLoader.TerrariaOutOfDateMessage"));
	break;
```
 
**Main.TML.cs, Line 394**

 ```
 if (!Directory.Exists(vanillaContentFolder)) {
	ErrorReporting.FatalExit(Language.GetTextValue("tModLoader.ContentFolderNotFound"));
}

// Canary file, ensures that Terraria has updated to at least the version this tModLoader was built for. Alternate check to BuildID check in TerrariaSteamClient for non-Steam launches 
if (!File.Exists(Path.Combine(vanillaContentFolder, "Images", "Projectile_981.xnb"))) {
	 ErrorReporting.FatalExit(Language.GetTextValue("tModLoader.TerrariaOutOfDateMessage"));
}
```

to


```
 if (!Directory.Exists(vanillaContentFolder)) {
//	ErrorReporting.FatalExit(Language.GetTextValue("tModLoader.ContentFolderNotFound"));
}

// Canary file, ensures that Terraria has updated to at least the version this tModLoader was built for. Alternate check to BuildID check in TerrariaSteamClient for non-Steam launches 
if (!File.Exists(Path.Combine(vanillaContentFolder, "Images", "Projectile_981.xnb"))) {
//	 ErrorReporting.FatalExit(Language.GetTextValue("tModLoader.TerrariaOutOfDateMessage"));
}
```

Okay, we are not done yet, the last thing is that you need to Copy the Content folder from "\Steam\steamapps\common\Terraria\Content" to "\Steam\steamapps\common\tModLoaderDev".


---


Thanks for reading my first post, hope you guys enjoyed :)


