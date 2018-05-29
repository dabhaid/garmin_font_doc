# What is this

This project started as a blast of inspiration delivered unwittingly by the amazing graphic and visual designers I work with. I wasn't a font geek, but <a href="https://fonts.google.com/specimen/Space+Mono">Space Mono</a>: hot damn. 

So I decided I wanted to replicate some of what I'd seen as a Garmin watch face for my new 645, celebrating Space Mono.

I am not a Garmin Connect IQ developer, so I started following documentation.

## Prerequisites
The first issue was Garmin devices only deal with bitmap fonts, and the <a href="https://developer.garmin.com/connect-iq/user-experience-guide/page-layout/#userfonts">Garmin Developer Guide on fontso</a> helpfully directs you to download a .exe, the <a href="http://www.angelcode.com/products/bmfont/">Bitmap Font Generator</a>. 

I tried using a bunch of alternatives, but everything seemed to generate bitmap fonts in formats that the Garmin Connect IQ build system did not like, so in the end I resorted to installing <a href="https://www.winehq.org/">WINE</a> using <a href="https://brew.sh/">Homebrew</a>, and running the Bitmap Font Generator there.

## Garmin Font fff...futzing
I wanted to have some of my text rotated 90 degrees clockwise. The layout primitives in Connect IQ are fairly primitive, so you don't get to apply transformations. Garmin provide <a href="https://developer.garmin.com/index.php/blog/post/connect-iq-pro-tip-custom-fonts-tricks">this helpful guide to custom fonts</a> which indicates you should manually rotate your glyphs, but doesn't tell you _how_ to do so.

## How to do so
### Rotating Fonts on Mac using Font Forge
On Mac the thing that finally worked for me was downloading and using <a href="https://fontforge.github.io/en-US/downloads/mac/">Font Forge</a>.

In there you can 
1. open your .ttf file
2. select the glyphs you want to rotate
3. right-click -> transform
4. select 'rotate' from the dropdown and choose your amount

Now the glyphs will appear rotated in the preview. You will be prompted to do

5. 'Element' -> 'Add extrema', I don't know what this does, so I just complied.

At this point your glyphs will look good in the preview, but there will be issues when you export because the glyphs are now too wide for the width allocated them. 

6. 'Metrics' -> 'Auto width...' and 
7. 'Metrics' -> 'Center in Width' together fixed the issue enough for me to proceed.

Now, bmfont on WINE on Mac (the tool we will use to generate bitmap fonts) can only read system fonts, so this means we need to install our font. To avoid having our weird rotated font replace the un-rotated font you started from, it's necessary to customize our new rotated fonts' info.

8. 'Element' -> 'Font Info' will bring up a dialog where we can change the name of our font.
9. Changing the 'Fontname', the 'Family Name', and the 'Name For Humans' in 'PS Name' and
10. Check that this has been reflected in 'TTF Name' - the extra thing I changed here was 'Styles' so my font only shows a custom style - it's clear this isn't a proper font when browsing Fontbook.
At this point you can try generating a font using

11. 'File' -> 'Generate Fonts', and generate a True Type font.

### Install on your system
Now double click on the generated ttf to open it in Fontbook, and install it if everything looks ok.

Once installed it will be discoverable in bmfont, and the reason we changed the name and family was to make it easy to find in BMFont.

### Using BMFont
Right click bmfont.exe and open with WINE. 

From there you can go 

12. 'Options' -> 'Font Settings' and pick your font, setting the size you want it to be when you export to bitmap.
13. 'Options' -> 'Export Options' and export textures as .png and finally
14. 'Options' -> 'Save bitmap font as...'

Congratulations, with a bit of luck you will have a rotated font you can use on your Garmin Watch Face.




