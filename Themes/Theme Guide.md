# How to make themes for Nuvola
With the new UI update being nearly ready for release, here is a complete guide to making themes for Nuvola.

## Where themes go
All theme files are loaded from `%LOCALAPPDATA%\Packages\Microsoft.MinecraftUWP_8wekyb3d8bbwe\RoamingState\Nuvola\Themes`. Place theme files here when downloading them manually.
***Furthermore, remember to add the `ALL_APPLICATION_PACKAGES` security group in the file properties or else the file will not load!!*** 

## The 4 theme sections
There are 4 main sections to a theme file. These are the metadata (the "meta" object), the icons, variables, and of course colors. All of these sections are technically optional, however without all of them the theme is incomplete.

## The format
Themes are JSON files with comment support. This means you can use `// Comment` or `/* Comment */` in your theme file. This can help users configure your theme file to their liking. The file will be a JSON object, so all of your theme data must be inside of brackets `{ /* Theme data */ }`.

## Metadata
The `meta` json object has information about the theme file itself. This information must include the theme's name, and who created it. Any additional information can be provided there as well, but at this moment there is no use of any additional data. This will likely change in the future.

Example `meta` block:
```
{
    "meta": {
        "name": "Nuvola Dark",
        "author": "DisabledMallis"
    },
    /* Other theme data */
}
```

## Icons
The `icons` json object allows you to specify which FontAwesome5 icons to use. You can search for icons [here](https://fontawesome.com/v5/search). When you find an icon you want to use, select the 'glyph' option in the top right, and paste that hex code into your theme. Each icon can also be a json object instead of just a string for the glyph id. This allows you to specify the size and position offset using the `size`, `offset_x`, `offset_y` and `glyph` fields respectively. This is important because sometimes the font renderer cannot accurately calculate the width & height of an icon, so you can adjust that manually to mitigate.

Example `icons` block:
```
{
    "icons": {
        "COMBAT": "f255",
        "RENDER": "f1b2",
        "MOTION": "f554",
        "PLAYER": "f007",
        "MISC": "f0ad",

        "ADD": {
            "glyph": "f067",
            "size": 14.0
        },
        /* Remaining icons */
    },
    /* Other theme data */
}
```

## Colors
The `colors` json object allows you to specify the colors of different parts of the ui. Colors are in the format of hex color codes. This means that `#FF0000FF` is red, `#00FF00FF` is green and `#0000FFFF` is blue. You can also specify transparency with the last byte, which makes `#00000000` completely transparent.

Example `colors` block:
```
{
    "colors": {
        "BUTTON_COLOR": "#00000000",
        "BUTTON_ACTIVE": "#0C0C0E00",
        "BUTTON_HOVERED": "#1C1C1EFF",
        /* Remaining colors */
    },
    /* Other theme data */
}
```

## Textures
The `textures` json array lets you specify base64 encoded image data for images used within the client. This section is optional, and a theme can be complete without it. The index of each texture object specifies what the image is used for. 

**NOTE: Only the PNG image format is supported at this moment. Many PNG image encoders add a block that looks like `data:image/png;base64,` to the data, which must be removed.**

Texture indexes
`0` - This is the first image in the array, and it is used for the client mascot (usually a picture of Nuvola).
`1` - This is the theme's icon, which will show on the theme's tile if specified.

Example `textures` block:
```
{
    "textures": [
        {
            "data": "/* Base64 encoded PNG data */"
        }
    ]
}
```

## Testing and debugging
Nuvola has a ThemeDebugger module (found under the Render category) that displays any errors and warnings a theme had while loading.