# Lenovo-M900-Tiny-Hackintosh-Sequoia

Information/Tutorial for my own Lenovo ThinkCentre M900 Tiny Hackintosh setup.

*DISCLAIMER\!*

I am not an authority on Hackintoshes in any way, as I have only gotten into them recently out of curiosity. All the information here is what I myself have gathered searching through countless tutorials, forum threads, etc. and I will be crediting whenever possible. Information here may not be entirely accurate, but as long as you have a M900 like myself everything here should be concrete steps on how to get Sequoia on there.

*VERSION CHANGES*

**V0.5 (1/20/2025)**

- Launch of tutorial  
- Basic steps included, pictures/video will be added eventually  
- 

*STEP \-1: WHAT YOU NEED AND SPECS*

What is inside my Lenovo ThinkCentre M900:

- CPU: Intel i5-6500T @ 2.5GHz  
- GPU: Intel HD Graphics 530 (integrated)  
- 16GB DDR4 RAM @ 2133MHz  
- BIOS Version FWKTBFA  
- Intel Dual Band Wireless-AC 8260

What you need for a Sequoia Hackintosh:

- This tutorial  
- 16GB minimum flash drive (Can do 32 to be sure)  
- Preferably NOT Intel Wifi cards as they apparently cause issues  
- Time and patience

*STEP 0: BIOS CONFIGURATION*

Before anything OS-related, use this [video](https://www.youtube.com/watch?v=u2KaYy_93QI) by [TechNolli](https://www.youtube.com/@TechNolli) and follow along with the BIOS setup to the best of your ability (timestamp for the configuration is 8:05-10:45.) You may be missing some settings but as long as you are able to copy most one for one you should be ready to install macOS on your system.

*STEP 1: INSTALLING WINDOWS*

Yes, for this tutorial I advise installing Windows first. It may not make sense but the ease of access to files that Windows provides (either through admin access or free downloads) makes it incredibly easy to understand what is happening behind the scenes AND gives you a safe haven in case your macOS install goes sideways. There are no tricks to the installation either, I used Windows 10 and partitioned around 200GB of my 2TB SSD for the install. After you reach the desktop, download DiskGenius, balenaEtcher, rEFInd and whatever .raw of version of macOS you want to install (I personally used Olarilla.) If you don’t know what any of that means just yet, don’t worry  as they will be explained as I go further along.

*STEP 2: INSTALLING rEFInd*

Now, some other tutorials don’t even have this as a step, and even OpenCore’s team advises against using rEFInd with OpenCore as they basically have the same function, as well as implying security risks if you do so. I am not well equipped enough to make a judgement call for you on that, so if it is a deal breaker I would assume you can still follow this tutorial just installing OpenCore, but for those without multiple machines or multiple drives or whatever their case may be, [rEFInd](https://sourceforge.net/projects/refind/files/0.14.2/refind-bin-0.14.2.zip/download) will basically act as your safeguard in case of any changes you make not allowing you access back into your macOS. Now earlier, I asked those following along to download DiskGenius, and that will come into play now installing rEFInd. DiskGenius will allow you to see all your drives and every partition on them. It will look scary and daunting, but what we are doing only requires a few steps. Extract the rEFInd .zip that you downloaded, and that will allow you to see the folder “refind”. This folder is what we are going to be copying over. Back to DiskGenius, find the drive you currently have Windows on and then right click the ESP partition. This will open up a dropdown, and you want to click the hide/unhide button and save your changes. Afterwards, you should be able to see the ESP partition in your File Explorer. All normal, navigate now to your rEFInd folder that you extracted, and you are going to want to place that in the partitions EFI folder, next to Boot and Microsoft. Before you exit DiskGenius, hover over Tools in the taskbar and at the bottom you can set your BIOS boot entries from here. Add the rEFInd\_x64.efi to the Boot Entries and move it to the top, save your changes and then boom\! rEFInd should be properly installed on your machine and it should be your top boot priority. Confirm this is the case with a restart or two, and then we can get into making the OpenCore Sequoia USB.

*STEP 3: CREATING THE USB INSTALLER*

This part contains mostly waiting, but install balenaEtcher and flash from file, selecting the .raw of your choice. Select your USB that has been formatted to FAT32 specifically, and I’m doubling up and making sure your USB is formatted to FAT32 because it only works with FAT32. Once formatted to FAT32, flash away and wait\! My flashes ran me around 30-45 minutes, I don’t know how that compares with the rest but it was never unbearable. Once done, you are actually not done\! You must copy the OpenCore EFI folder over the one that was made on your USB. DELETE THE EFI FROM THE USB, AND THEN COPY THE OPENCORE EFI. You don’t want any part of the native macOS .efi to be interacting with the OpenCore one, and all tutorials now including mine advise deleting the folder outright and then copying over. Once the OC .efi is pasted completely, you are done\! This USB can act as another safeguard against changes made to your macOS, but that is information for later.

*STEP 4: INSTALLING macOS*

This is the moment you’ve been waiting for. Plug that USB into the front, turn on your M900 and behold rEFInd. Select OpenCore.efi and it should pop up with another boot manager, OpenCore. It looks sleek and professional, and you should see an option to install your version of macOS. Click/Select it, and hopefully you have been greeted with the homepage of the installer. You will see multiple options but before I go further, those who want a specific size for this OS should be booting into Windows first and creating a NTFS partition to act as a placeholder. This will make sense as either way you should head into Disk Utility first. If you are using your entire drive, erase such and then create a new partition with APFS, and those using a specific size do the same thing but for your designated NTFS partition you made in Windows. Once complete, you can continue with the installer. Select the correct partition you have made and then wait as macOS installs. It will probably restart multiple times throughout the process, and just allow it to reboot and keep opening OpenCore via rEFInd.  A new pop-up will appear, macOS installer. Click/Select that option and the installation will continue, along with more restarts. Just keep opening that macOS Installer option and then eventually, it should become the name of the partition. macOS has been successfully installed onto your machine\!