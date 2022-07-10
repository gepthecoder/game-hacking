# game-hacking
Documentation on how to exploit android, unity games 🐱‍💻

STEP BY STEP GUIDE ON HOW TO EXPLOIT UNITY AND ANDROID GAMES/APPS


#
# GENERAL TOOLS SETUP
#
git clone https://github.com/gepthecoder/game-hacking

cd game-hacking
#
In main directory you'll find HexEditor, APKTool, dnSpyware & Il2CppDumper. Extract contents of zip files and install APKTool & Hex Editor of your choice.
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
H&D Hex Editor - A hex editor (or binary file editor or byte editor) is a computer program that allows for manipulation of the fundamental binary data that constitutes a computer file. 
#

#
# ANDROID APKs - IL2CPP 32-bit
#

1.) Find a mobile game on Google Play Store

2.) Copy Link and navigate to apkpure.com | apkgk.com (generate apk based on device 32bit or 64bit) | apkmirror.com 

3.) Paste link into search box and it'll pull up the specific apk with available versions - Download it

4.) Common practice is to create a BACKUP File, once you did that open the apk file with your favourite archiver: 7zip, winzip, winrar etc..

5.) Create Internals folder and find the 32bit - armeabi-v7a/libil2cpp.so located in libs folder -> drag&drop it to Internals folder you have just created.

6.) Go to assets/bin/Data/Managed/Metadata and copy the global-metadata.dat file into Internals folder. Boom we are good to go to DUMP the files.

7.) Copy the extracted Il2CppDumper content into Internals folder.

8.) Run Il2CppDumper-x86.exe and select libil2cpp.so file first, then the global-metadata.dat

9.) Success! After the dump is done, you can access dlls in generated DummyDll folder.

10.) Open dnSpy.exe and drag&drop Assembly-CSharp.dll into the Assembly Explorer.

11.) Note: you will not get code from idle to cpp, that means you cannot get it and compile it back.

12.) At the same time open the libil2cpp.so with the hex editor of your choice (simply drag it to hex editor).

13.) You can find the C# to armeabi-v7a on the bottom of this document.

















#
# C# TO ARMEABI-V7a 32-bit
#
#Always Return True as a Boolean

What is a Boolean:
A Boolean is simply a True or False statement. Without realizing it, you think with bool’s in your day to day life, so these are easy to understand. They’re, in a sense, the same as a Yes or No question/answer. If someone asks you  “Can you please pass the butter?” at dinner, Yes would be the same as “true”, No would be the sale as “false!”

C# Code

public bool true() {
return true;
}

IDA/HEX Code

MOV R0,#1
BX LR
Hex: 01 00 A0 E3 1E FF 2F E1

#Always Return False as a Boolean

What is a Boolean: See above

C# Code

public bool false() {
return false;
}

IDA/HEX Code

MOV R0,#0
BX LR
Hex: 00 00 A0 E3 1E FF 2F E1

#Force Freeze a Number/Int

What is an Int:
Int stands for Integer which is just a fancy word for a basic number. These numbers can come in multiple “flavors” of Int8, Int16, Int32 and Int64. Depending on how high of a number the game needs to display will determine which Integer type is declared. In 90% of IL2CPP hacking I’ve personally done, the only time I see Int64 is when its used for Time. Other than that, I always see Int32 or Int16. Either should work with the code below.

C# Code

public int oInt() {
return 999;
}

IDA/HEX Code

MOV R0, #999
BX LR
Hex: E7 03 00 E3 1E FF 2F E1

#Hex for Unlimited Money Int:

01 04 A0 E3 1E FF 2F E1
Force Freeze a Float Number/Int

What is a Float Number/Int:
As stated above, an Int, aka an Integer, is a fancy word for a number. Although, a Float Int is far different from a boring old Int32. A Float is used in the situation of a number that is constantly changing. For example, in a game where you have a set amount of Race Boost but it depletes as you use it, the number from Max Boost to 0 would be set as a Float as its constantly changing as you earn it or use it. In C# programming, you can tell the simple difference between a Float and a basic Integer simply by if there is a lowercase “f” after the number like below.
You CAN NOT use Hexidecimal number values longer than 4 characters… for example, you could change this to 437B, but not 437BA.

C# Code

private float oFloat()
{
return 999f;
}

IDA/HEX Code

MOV R0, #0x447A
BX LR
hex -> 7A 04 04 E3 1E FF 2F E1

