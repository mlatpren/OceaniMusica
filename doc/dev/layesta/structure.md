# Layesta file format
## Part 1: file structure

Layesta's charts come in the form of `.layesta` files. These files can be either downloaded in Layesta itself, or downloaded from somewhere on the Internet and imported. When making a chart for Layesta, this is the file format the chart must be saved in.

### Overall structure

A `.layesta` file goi ko'a is deceptively simple. It's just a `.zip` file with the extension changed. It's not like this is unusual; other common examples of this are `.apk` files (Android executables) and `.java` files (Java executables). I think `.exe` files .a `.msi` files do something similar. After unzipping ko'a, its contents are revealed.

### Background(s)

There's a file titled `background.png` that's used for the background as the chart is playing. It's a normal `.png` file with a resolution of 720x1280. If the background is NSFW, there will also be a blurred varient, called `background_blur.png`. The only difference is that this background was sent through a rather strong blur filter. 

### chart file

This one has a lot of meat. For more than an overview, cf. `chart-file.md`.

This file is the heart of the chart. It contains almost all the data, including the notes. It's a `text/json` file with the extension `.txt`. Why this is the case, I don't know. The file is completely void of whitespace, and HUGE. My current reference file is 338 KiB (or exactly 346,004 bytes). It's split into a few parts:

- `"events"`: An array of objects, each with a `"type"` attribute ranging from 0-13. This holds the data for notes, tuner movements, and setting the chart defaults. It makes up almost the entire file.
- `"eos"`: A floating-point number, indicating how long the song is in seconds. Its precision goes to milliseconds (in the thousandths place).
- `"bpm"`: I'm not sure what this is, but it's structured like `"events"`, with the camera data missing. `"type"` in my reference file is only 0 or 6 for these. Only one of them is 6, and it's the first one. Maybe it's like 12 for `"events"`, where it sets the defaults?
- `"scroll"`: An array of objects, each containing `"speed"` and `"timing"`, both floating-point numbers. Other than that, I don't know what this is.

### Metadata

There's a metadat file called `info.bytes`. I don't know if its structure fits a standard. It contains, from what I can tell, 4 peices of information:

- `(%s)` The song name  
- `(%a)` The artist     
- `(%d)` The difficulty 
- `(%c)` The charter    

In `/bin/date` fashion, below is what it'd look like if you wanted to print out the hex data for `info.bytes`, based off my reference file. See the `%` codes in the list above:

`06 %s 08 %a 01 00 00 00 06 %d 00 05 00 00 D0 02 00 00 04 %c 02 00 00 00`

### Music

The last file is a(n) `audio/mp3` file. This is the actual song that gets queued up when the chart's played. I'm not sure if there's any requirements for the file, but my sample file has the following data, according to VLC:

- Bitrate: 192 KB/s
- Codec: MPEG Audio Layer 1/2
- Channels: 2
- Sample rate: 44100 Hz

### References

Currently, I only have one reference file, so this may not all be correct. The reference file I was given is titled `SPOILER_Hentai.layesta`. I think the `SPOILER_` part was added by Discord, since it was marked as a spoiler, because the `info.bytes` file simply says `Hentai`. As I work on this project, I'm going to get more and more ko'a, so I'll have more references to work off of. I'll also be progressing through reading Layesta's code to have a better understanding of ko'a. This file will be updated as I learn more things. 
