# Minecrafted Smooth Terrain

This is a set of modified files which make Roblox's smooth terrain appear like the voxel terrain seen in Minecraft. The modification only works offline and won't appear if you publish a game with the terrain modified. It was just a fun experiment to see how flexible Roblox's terrain material configurations are.

## Setup

Copy the `terrain` and `textures` folders into the `PlatformContent\pc` folder in Roblox Studio's runtime directory. You'll also need to go to `File > Studio Settings...`, and under the `Rendering` tab, make sure `ReloadAssets` is checked.

## Bug Workaround

When you open a place with the modified terrain, the terrain likely won't be using cubes immediately. This is a bug on Roblox's end, but you can work around it by applying any change to the `materials.json` file. Just put a space next to a comma, save the file, and that'll force Roblox to refresh and correctly pick up on the cubified configuration!

## Resources used to edit

I primarily used Visual Studio 2019 to edit the textures. It has a built-in toolset for editing DDS images as well as auto-generating the necessary mipmaps for `diffuse_array.dds`. The colorspace of the original textures had to be converted from RGB to YCoCg, so I wrote a quick program in C# to do so.

Roblox's conversion from RGB->YCoCg can be described as such C#:

```cs
private static Image to_YCoCg(Image image)
{
    var bitmap = new Bitmap(image);

    for (int i = 0; i < bitmap.Width; i++)
    {
        for (int j = 0; j < bitmap.Height; j++)
        {
            Color color = bitmap.GetPixel(i, j);

            int r = color.R,
                g = color.G,
                b = color.B,
                a = color.A;

            int co = r - b;
            int tmp = b + (co / 2);

            int cg = g - tmp;
            int y = tmp + (cg / 2);

            Color newColor = Color.FromArgb(a, 127 + (co / 2), y, 127 + (cg / 2));
            bitmap.SetPixel(i, j, newColor);
        }
    }

    return bitmap;
}
```
