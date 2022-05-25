---
title: How to Fix a Bricked Kindle
date: 25-05-2022
private: false
---

** NOTE: **  This process will completely reset your kindle to factory settings.

1. Plug your kindle into your computer.
2. Navigate to the root directory:
  - Terminal on Mac: `cd /Volumes/kindle`
  - Finder: Locations (on the left) then "kindle"
  - File Explorer: This PC -> kindle
3. Add an extension-less file `DO_FACTORY_RESTORE` to the root of the kindle.
  - On windows, open notepad and make a new file called "DO_FACTORY_RESTORE", copy that to the kindle directory and **MAKE SURE** to remove the `.txt` extension.
  - On Mac, `cd` into the kindle directory and `touch DO_FACTORY_RESTORE`, EZ.
4. reset your kindle by holding down the power button for 40 seconds.
5. Setup your kindle.
