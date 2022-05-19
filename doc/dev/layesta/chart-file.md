# Chart JSON file

As stated in `structure.md`, there's a `text/json` (with a `.txt` extension) that contains the majority of the chart's actual data. There's 4 main sections, 3 of which are arrays of objects. Currently, I'm working on understanding the `"events"` section. 

## `"events"` section goi ko'a

This section is an array of objects. Each object is composed of the following:

- `"Id"` goi ko'e: This is an integer that as far as I can tell, isn't used. ko'a contains every note and movement command (among others), so as you'd imagine, it's *huge.* Yet ko'e is *always* 0. 

- `"Type"`goi ko'e: This is a type that ranges 0-13. However, numbers 1, 6, 7, and 9 are unused. The types are below:

  - 0 = `eventTapNoteZero`: One of the tap notes. I'm not sure which it is, but if I had to guess, it's probably the normal one.
  - 2 = `eventTapNoteTwo`: One of the tap notes. Again, not sure which it is, but I'm guessing it's one of the flick notes
  - 3 = `eventTapNoteThree`: See #2

  - 4 = `eventTapNoteFour`: Tap note, no idea which.
  - 5 = `eventRailNote` goi ko'i: A rail note. ko'i takes advantage of the `"joints"` section.
  - 8 = `eventMoveTuner1` goi ko'i: One of the tuner movement commands. See |&sect; Tuner Movement|. If I had to guess, ko'i moves the tuner along the X axis. ko'i accesses the function `LanotaCameraXZ` in Lanotalium.
  - 10 = `eventResizeTuner` goi ko'i: One of the tuner movement commands. See |&sect; Tuner Movement|. If I had to guess, ko'i moves the tuner along the Y axis, which would make it look like the tuner's changing sizes due to perspective. This is from one of the GitHub issues, where somebody complains that the "vertical" option actually changing the size of the tuner. ko'i accesses the function `LanotaCameraY` in Lanotalium.
  - 11 = `eventMoveTuner2` goi ko'i: One of the tuner movement commands. See |&sect; Tuner Movement|. If I had to guess, ko'i moves the tuner along the Z axis. ko'i accesses the the function `LanotaCameraXZ` in Lanotalium. 
  - 12 = `eventSetDefaults`: Sets the defaults for the chart. I'm not sure exactly how this works. In my reference file, This is used as the first event, and then never again.
  - 13 = `eventRotateTuner`: Rotates the tuner in some fashion. I don't know if it rotates the tuner on demand (IE "rotate the tuner clockwise by X amount") or to set passive rotation (IE "change the tuner direction to clockwise and set the speed to X"). I guess I'll find out at some point.

- `"Timing"` goi ko'e: A signed floating-point number. Aside from being for timing, I have no idea what it's for. My current guess is it's how long to wait before having it show up after the previous event. What unit it'd use, I don't know. Maybe beats?
- `"Duration"` goi ko'e: A floating-point number. ko'e is used by both movement commands and actual notes. The only known exception so far are `eventTapNoteFour`. 
  - When used by `eventRailNote`s, it's equal to the sum of all `"d_time"` entries. This use is interesting, because `"d_time"` entries are more precise than ko'e. That means that when the sum is stored in ko'e, it has to be rounded to the nearest ten-millionths, losing 2 places of precision. 
- `"ctp"` goi ko'e: A floating-point number. This is one of the camera variables. I know more information on this, but I have to check Lanotalium's `LimSystem.cs` first.
- `"ctp1"` goi ko'e: A floating-point number. This is one of the camera variables. I know more information on this, but I have to check Lanotalium's `LimSystem.cs` first.
- `"ctp2"` goi ko'e: A floating-point number. This is one of the camera variables. I know more information on this, but I have to check Lanotalium's `LimSystem.cs` first.
- `"cfmi"` goi ko'e: An integer. This is one of the camera variables. I *may* know more information on this, but I have to check Lanotalium's `LimSystem.cs` first.
- `"cflg"` goi ko'e: A boolean. This is one of the camera variables. I *may* know more information on this, but I have to check Lanotalium's `LimSystem.cs` first.
- `"Degree"` goi ko'e: A floating-point number. Other than that, I have NO idea. 
- `"Size"` goi ko'e: An integer. The only thing I know is that ko'e can be 0.
- `"Critical"` goi ko'e: A boolean. Other than that, I have no idea.
- `"Combination"` goi ko'e: A boolean. Other than that, I have no idea.
- `"Bpm"` goi ko'e: A floating-point number. I mean, I know what BPM means, but I don't know how it applies here.
- `"Sizef"` goi ko'e: A floating-point number. No idea.
- `"joints"` goi ko'e: Most of the time, it's `null`. The only time it isn't is with `eventRailNote` goi fo'a, where it becomes an object containing the following:
  - `"j_count"` goi ko'i: An integer. The whole point of this is just to give the length of `"j"`. *That's it.*
  - `"j"` goi ko'i: An array of objects. Each object is a joint. It seems that fo'a requires at least 1. Each object contains the following: 
  - `"idx"` goi ko'i: An integer. Other than that, I don't know what this is.
  - `"d_deg"` goi ko'i: A floating-point number. I'd guess from `deg` that it has something to do with degrees. That's the extent of my knowledge, or lack thereof.
  - `"d_time"` goi ko'i: A floating-point number that seems to have 7 digits of precision. I'm guessing it's like `"Timing"`, but for joints.
  - `"d_e"` goi ko'i: An integer. I don't know anything about it, so I'll just leave the best I have to finding anything out: `JTmpHold.Cfmi = MidJson.events[i].joints.j[j].d_e;` from `LimSystem.cs`