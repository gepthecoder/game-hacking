# game-hacking
Documentation on how to exploit android, unity games 🐱‍💻

STEP BY STEP GUIDE ON HOW TO EXPLOIT UNITY AND ANDROID GAMES/APPS


#
# GENERAL TOOLS SETUP
#
git clone https://github.com/gepthecoder/game-hacking

cd game-hacking
#
In main directory you'll find HexEditor, APKTool, dnSpyware & Il2CppDumper. Extract contents of zip files and install APKTool & Hex Editor of your choice on your computer.
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

![image](https://user-images.githubusercontent.com/38008294/178573632-450cade6-fad5-40a9-a20f-2e03c4765084.png)

3.) Paste link into search box and it'll pull up the specific apk with available versions - Download it

![image](https://user-images.githubusercontent.com/38008294/178573509-ecdc4c2f-a677-4be4-b32a-1705427dd427.png)

4.) Common practice is to create a BACKUP File, once you did that open the apk file with your favourite archiver: 7zip, winzip, winrar etc..

![image](https://user-images.githubusercontent.com/38008294/178574288-992dd651-b96e-4364-8f75-942c92d82ed3.png)

5.) Create Internals folder and find the 32bit - armeabi-v7a/libil2cpp.so located in libs folder -> drag&drop it to Internals folder you have just created.

![image](https://user-images.githubusercontent.com/38008294/178574711-623e5b31-9e17-4259-a6fc-e30e5e8b6927.png)

6.) Go to assets/bin/Data/Managed/Metadata and copy the global-metadata.dat file into Internals folder. Boom we are good to go to DUMP the files.
 
![image](https://user-images.githubusercontent.com/38008294/178574783-f2dcf3db-a724-456f-bb7a-4e27e31d7d3c.png)

7.) Copy the extracted Il2CppDumper content into Internals folder.

8.) Run Il2CppDumper-x86.exe and select libil2cpp.so file first, then the global-metadata.dat

![image](https://user-images.githubusercontent.com/38008294/179053041-45ddbe9b-a9f8-43e1-af9b-3e96553bb9a1.png)

![image](https://user-images.githubusercontent.com/38008294/179053238-1a86d9db-ed00-4083-9da7-8226c61cfae4.png)

![image](https://user-images.githubusercontent.com/38008294/179053264-9a37cfaa-f310-4f9d-91e5-81ee27c59909.png)

9.) Success! After the dump is done, you can access dlls in generated DummyDll folder.

![image](https://user-images.githubusercontent.com/38008294/179053412-4aa18186-5295-47e8-a32c-b1016070dcfa.png)

10.) Open dnSpy.exe and drag&drop Assembly-CSharp.dll into the Assembly Explorer.

![image](https://user-images.githubusercontent.com/38008294/179053835-9f4dd06c-012c-48b7-87b4-4e638b18e6e8.png)

11.) Note: you will not get code from idle to cpp, that means you cannot get it and compile it back. Soo...

12.) At the same time open the libil2cpp.so with the hex editor of your choice (simply drag it to hex editor).

![image](https://user-images.githubusercontent.com/38008294/179054686-92ab3483-51db-43c2-8e73-91dc834d7a99.png)

13.) You can find the C# to armeabi-v7a reference info on the bottom of this document.

14.) To start expoloiting the app you need to find vunreabilities in the dll via dnSpy software.

![image](https://user-images.githubusercontent.com/38008294/179053714-05678915-bb1a-48cb-a557-c08b6025f58b.png)

15.) Once you found what you want to manipulate, open hex editor window and search for the function address location - CTRL+G

![image](https://user-images.githubusercontent.com/38008294/179055094-c5bb53c5-817e-4bd5-a22e-dff9e074abd9.png)

![image](https://user-images.githubusercontent.com/38008294/179056185-f33ea5e3-712c-4f44-9bdf-4d73284c1b64.png)

![image](https://user-images.githubusercontent.com/38008294/179056772-47403d7a-a6ec-4ebd-ad99-7b2d92ba3b80.png)

16.) Extrapolate the desired float - hex code above and apply it to the existing hex file with CTRL+B

![image](https://user-images.githubusercontent.com/38008294/179057424-3033cca9-f8b7-49cd-9bbc-9742738e673f.png)

17.) When you are done, dont forget to save it and replace the libil2cpp.so file in the apk directory.

![image](https://user-images.githubusercontent.com/38008294/179057616-9fcf500f-016a-45c3-ba39-0b9fe31f57a9.png)

18.) The final step is to open APK Easy Tool and sign the newly updated apk.

![image](https://user-images.githubusercontent.com/38008294/179058164-fd54d556-c91d-455d-b497-25f91fa8c7a2.png)

19.) Have a beer, you have done it! ;) 

#
# UNITY STANDALONE - MONO
#

Reverse engineering unity games with monobehaviour scripting backend is quite easy and straightforward.

1.) The first step is to find / download a PC game made in unity

![image](https://user-images.githubusercontent.com/38008294/179343930-e5c553b0-c539-4e13-87b7-762190a21c67.png)

2.) Navigate to App/AppData/Managed directory where you'll find the Assembly-CSharp.dll file.

![image](https://user-images.githubusercontent.com/38008294/179344001-8caec3d9-ff3c-4ab3-9221-5e5e18d4670a.png)

3.) Open dnSpy software and select the chosen dll.

![image](https://user-images.githubusercontent.com/38008294/179344065-f0225a38-cc79-4018-a247-13193ec2dab8.png)

4.) Start exlploring for vulnerabilities

![image](https://user-images.githubusercontent.com/38008294/179344102-e09e14c8-4977-4369-96b2-0e40456c531f.png)

5.) Mono is not secure at all.. as you can see, the code is fully accessable and ready to be modded ;)

![image](https://user-images.githubusercontent.com/38008294/179344197-d3d4604a-c46b-4ae6-b81d-9a5a70eca188.png)

6.) Right click on a method / class / object you want to change and hit edit with c#

![Documentation](https://user-images.githubusercontent.com/38008294/179344297-293ef6ed-70d7-41ae-ba16-afb2d3ae79ce.png)

7.) Program your way into anything basically.. 🥷

![image](https://user-images.githubusercontent.com/38008294/179354854-3ef35b49-1e89-4848-b273-0d36ab0e7bc9.png)

![Documentation1](https://user-images.githubusercontent.com/38008294/179354926-57d6e962-85bb-4717-b1d4-1ca72b828344.png)

8.) Dont forget to save your hacked module version

![Documentation2](https://user-images.githubusercontent.com/38008294/179354962-8c831dba-5bed-470c-a73b-e482a6c725df.png)

9.) Have fun! 😅


#
# C# TO ARMEABI-V7a 32-bit
#
# Always Return True as a Boolean

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

# Always Return False as a Boolean

What is a Boolean: See above

C# Code

public bool false() {
return false;
}

IDA/HEX Code

MOV R0,#0
BX LR
Hex: 00 00 A0 E3 1E FF 2F E1

# Force Freeze a Number/Int

What is an Int:
Int stands for Integer which is just a fancy word for a basic number. These numbers can come in multiple “flavors” of Int8, Int16, Int32 and Int64. Depending on how high of a number the game needs to display will determine which Integer type is declared. In 90% of IL2CPP hacking done, the only time we see Int64 is when its used for Time. Other than that, I always see Int32 or Int16. Either should work with the code below.

C# Code

public int oInt() {
return 999;
}

IDA/HEX Code

MOV R0, #999
BX LR
Hex: E7 03 00 E3 1E FF 2F E1

Note: to apply any number go to decimalToHex converter. Example: 999 in hex is 03E7 so we substitute only first four hex 
numbers in reversed manner like the example above.

# Hex for Unlimited Money Int:

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

