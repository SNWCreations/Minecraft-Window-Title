# For Users

## Installation

The mod supports [Forge](https://files.minecraftforge.net/) and [Fabric](https://fabricmc.net/) (*) mod loaders, **the same mod file will work in both**. Follow either mod loader's installation guide, then [download the mod file](https://www.curseforge.com/minecraft/mc-mods/custom-window-title/files) for your Minecraft version, and install it into the **.minecraft/mods** folder.

(*) Fabric API is **not** required.

## Configuration

Run the game once to create the configuration file. By default, the window title will be set to **Minecraft _<version>_**. Unlike in vanilla 1.15.2 onwards, the title will not change when you enter a world/server.

To change the title or icon, navigate to the **.minecraft/config** folder, and open **customwindowtitle-client.toml** in a text editor. You will see the following entries:

```toml
title = 'Minecraft {mcversion}'  
icon16 = ''  
icon32 = ''
```

Only edit text inside quotes or apostrophes.

### Changing the Title

You can use the following special tokens in the _title_ configuration entry:

* **{mcversion}** - current Minecraft version
* **{modversion:<span style="text-decoration: underline;">modid</span>}** - version of installed mod with the identifier _modid_

If any of the tokens aren't working, search the game log for **CustomWindowTitle** and you should see the reason, otherwise please file an issue on the [issue tracker](https://github.com/chylex/Minecraft-Window-Title/issues) with as many details as possible.

### Changing the Icon

Create a square PNG image whose dimensions are a power of two, such as 32x32 or 48x48. Put the PNG file into the .minecraft/config folder, either directly or into a subfolder.

The icon **must be saved with transparency** even if it doesn't use it, otherwise the icon may be corrupted or not appear at all. In Krita, for example, you must check Store alpha channel (transparency) when saving.

The icon configuration entry points to the PNG file relative to .minecraft/config.

For example, if you placed the icon into .minecraft/config/customwindowtitle/icon.png, then the configuration entry should look like this:

```properties
icon = 'customwindowtitle/icon.png'
```

## Screenshots

These screenshots were taken using the following example configuration:

```toml
title = "Minecraft {mcversion} - Custom Window Title {modversion:customwindowtitle}"
```

![](https://github.com/chylex/Minecraft-Window-Title/blob/master/.github/README/screenshot.png)

# For Developers

The mod sources are organized into 3 projects:
- `src/` contains common source files and mixins
- `Fabric/src/` contains source files specific for Fabric
- `Forge/src/` contains source files specific for Forge

The Gradle project provides the following tasks:
- `setupIdea` generates Minecraft sources and run configurations for IntelliJ IDEA
- `assemble` creates 2 `.jar` files in the `build/dist` folder - one for Forge, one for Fabric

When building against a Minecraft version that is only supported by one mod loader, open `gradle.properties` and comment or remove either `forgeVersion` or `fabricVersion` to disable them.
