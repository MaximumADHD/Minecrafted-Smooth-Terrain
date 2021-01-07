# Minecraftified Smooth Terrain

This is a set of modified files which make Roblox's smooth terrain appear like the voxel terrain seen in Minecraft. The modification only works offline and won't appear if you publish a game with the terrain modified. It was just a fun experiment to see how flexible Roblox's terrain material configurations are.

## Setup

Copy the `terrain` and `textures` folders into the `PlatformContent\pc` folder in Roblox Studio's runtime directory. You'll also need to go to `File > Studio Settings...`, and under the `Rendering` tab, make sure `ReloadAssets` is checked.

## Bug Workaround

When you open a place with the modified terrain, the terrain likely won't be using cubes immediately. This is a bug on Roblox's end, but you can work around it by applying any change to the `materials.json` file. Just put a space next to a comma, save the file, and that'll force Roblox to refresh and correctly pick up on the cubified' configuration!