# ue4_pixel_art

![C64 in C64](/readme_assets/c64.png?raw=true "UE4 C64 iin C64")

**Important: This repo is highly unfinished.  The render_pixel_art PP material works nicely but for now anything else is suspect**

A set of useful UE4 stuff for pixel art.  When this is complete it will include using the res/palette of older machines, using grayscale images + palette, and producing the grayscale images automatically from colour sources.

At the moment this includes:

## render_pixel_art
This part of the Pixel Art setup allows you to take your scenes and render them in the style of an older machine, limiting itself to a specified resolution and palette.  For a simple example here's a basic level with a picture of a parrot rendered in the palette and resolution of a Commodore 64.

![UE4 C64 Parrot](/readme_assets/c64_parrot.png?raw=true "UE4 C64 Parrot")

To try things out open **demo_content/Parrot_Map**, choose the **render_pixel_art_bp** and for *Render Setting* choose one of the presets from the **render_settings** directory.

At present I've made no attempt to simulate [attribute clash](https://en.wikipedia.org/wiki/Attribute_clash), which limited the colours displayed in a character block on older hardware.  While I have some thoughts on how this could be done for now I'm just building something simple which looks good rather than delve into the complexities.

The files used for this include:

* **demo_content**: Just a simple test level, nothing too interesting.  Has a nice public domain picture of a parrot from [Wikipedia](https://en.wikipedia.org/wiki/List_of_8-bit_computer_hardware_palettes#/media/File:RGB_24bits_palette_sample_image.jpg), though, it's cute.  I call him Bob.

* **palette_images**: All of the palettes used for the system.  Where a system has multiple palettes, such as CGA, each row of the image is a separate palette which can be selected.

* **postprocess_masters**: The master implementation of the post-process effect to perform the rendering effect.  There's a separate one for each palette size, a larger one will work happily with a smaller palette but won't be as efficient.  Also includes **color_difference** which is a material function used to get the best colour match from two potential colours, and which is used repeatedly for each colour in a palette to find the best overall match.

* **render_settings**: Actual material instances of the masters in **postprocess_masters** intended to simulate a particular piece of hardware.  Currently has the following:
  * **c64_pp**: Commodore 64 palette (16 colours), 320x200 resolution
  * **cga_p0_pp**: CGA palette 0 (Black, Green, Red, Brown), 320x200 resolution
  * **cga_p0hi_pp**: CGA palette 0 (Black, Green, Red, Brown)in high brightness, 320x200 resolution
  * **cga_p1_pp**: CGA palette 1 (Black, Cyan, Magenta, Gray), 320x200 resolution
  * **cga_p1hi_pp**: CGA palette 1 (Black, Cyan, Magenta, Gray) in high brightness, 320x200 resolution
  * **teletext_pp**: Teletext palette (Black, White, Red, Green. Blue, Yellow, Magenta, Cyan), which is also the eight colours you get by setting red/green/blue to all combinations of maximum/minimum, and 72x69 resolution
  * **zx81_pp**: ZX81 palette (White/Black monochrome), 64x44 resolution

* **render_pixel_art_bp**: Blueprint for setting up the rendering system.  Turns off the tonemapper so it doesn't break anything, and then adds one of the setting files from **render_settings** to a post-process volume to turn the effect on.


## Thanks Go To...

* Warren Marshall for [the c64 model used in the title pic](https://www.unrealengine.com/marketplace/retro-gaming-mini-pack)

----

## LICENSE ([MIT License](https://en.wikipedia.org/wiki/MIT_License))

Copyright 2017 Paul Golds.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
