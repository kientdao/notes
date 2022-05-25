---
title: How to Fix a Bricked Kindle via USB
date: 25-05-2022
private: false
---

**NOTE:**  This process will completely reset your Kindle to factory settings.

1. Plug your Kindle into your computer.
2. Navigate to the root directory:
  - Terminal on Mac: `cd /Volumes/Kindle`
  - Finder: Locations (on the left) then "Kindle"
  - File Explorer: This PC -> Kindle
3. Add an extension-less file `DO_FACTORY_RESTORE` to the root of the Kindle.
  - On windows, open notepad and make a new file called "DO_FACTORY_RESTORE", copy that to the Kindle directory and **MAKE SURE** to remove the `.txt` extension.
  - On Mac, `cd` into the Kindle directory and `touch DO_FACTORY_RESTORE`, EZ.
4. reset your Kindle by holding down the power button for 40 seconds.
5. Setup your Kindle.
