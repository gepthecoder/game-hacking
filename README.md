# game-hacking
Documentation on how to exploit android, unity games 🐱‍💻

STEP BY STEP GUIDE ON HOW TO EXPLOIT UNITY AND ANDROID GAMES/APPS


#
# GENERAL TOOLS SETUP
#
git clone https://github.com/gepthecoder/game-hacking

cd game-hacking
#
In main directory you'll find APKTool, dnSpyware & Il2CppDumper. Extract contents of zip files and install APKTool
on your computer.
#
APK Easy Tool - is a lightweight GUI application that enables you to manage, sign, compile and decompile the APK files for the apps you are working on. Its used for reverse engineering 3rd party, closed, binary Android apps.
#
dnSpyware - is a debugger and .NET assembly editor. You can use it to edit and debug assemblies even if you don't have any source code available.

Credit: https://github.com/dnSpy/dnSpy
#
Il2CppDumper - Unity il2cpp reverse engineering tool - Supports Unity 5.3 - 2021.3 - Support bypassing simple PE protection

Credit: https://github.com/Perfare/Il2CppDumper
#

#
# ANDROID APKs - IL2CPP
#

1.) Find a mobile game on Google Play Store

2.) Copy Link and navigate to apkpure.com | apkgk.com (generate apk based on device 32bit or 64bit) | apkmirror.com 

3.) Paste link into search box and it'll pull up the specific apk with available versions - Download it

4.) Common practice is to create a BACKUP File, once you did that open the apk file with your favourite archiver: 7zip, winzip, winrar etc..

5.) Create Internals folder and find the 32bit - armeabi-v7a/libil2cpp.so located in libs folder -> drag&drop it to Internals folder you have just created.

6.) Go to assets/bin/Data/Managed/Metadata and copy the global-metadata.dat file into Internals folder. Boom we are good to go to DUMP the files.

7.) Copy the extracted Il2CppDumper content into Internals folder.

8.) 

