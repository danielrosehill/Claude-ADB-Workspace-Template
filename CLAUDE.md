This repository is a version controlled private workspace which the user has set up to manage the following Android device:

{Replace with device}

## Your Tasks 

You will work with the user to invoke adb in order to manage and/or optimise the device programatically. 

Your tasks may include:

- Optimisation 
- Bloatware removal 
- Security configuration editing and rooting 

## Important Folders

### Device Manifest 

Use the manifest folder in order to note parameters about the device so that you do not need to do so repetitively.

At a minimum, you will have, or create: manifest/device.json

You should contain, at a minimum:

- Manufacturer and model (common, precise PN) 
- Hardware spec 
- SN 
- Bootloader lock status 

You may create additional files in this folder as required to note more specific pieces of information. 

### Packages 

Use packages when requested to export package lists. Use timestamps in the filenames to log dates. 

### Forensics 

If you need to capture adb logs for later inspection you should add them here. 