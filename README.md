<a href="https://tinybiggames.com" target="_blank">![CPas Logo](media/logo.png)</a>

[![Chat on Discord](https://img.shields.io/discord/754884471324672040.svg?logo=discord)](https://discord.gg/tPWjMwK) [![GitHub stars](https://img.shields.io/github/stars/tinyBigGAMES/CPas?style=social)](https://github.com/tinyBigGAMES/CPas/stargazers) [![GitHub Watchers](https://img.shields.io/github/watchers/tinyBigGAMES/CPas?style=social)](https://github.com/tinyBigGAMES/CPas/network/members) [![GitHub forks](https://img.shields.io/github/forks/tinyBigGAMES/CPas?style=social)](https://github.com/tinyBigGAMES/CPas/network/members)
[![Twitter Follow](https://img.shields.io/twitter/follow/tinyBigGAMES?style=social)](https://twitter.com/tinyBigGAMES)

## Overview
What if you were able to load and use C99 sources directly from Delphi? There is a vast quantity of C libraries out there and being able to take advantage of them, without being a pain would be nice. You could even compile a bunch of sources and save them as a library file, then load them back in from disk, a resource or even from a stream. You can get the symbols, map to a C routine, and execute from the Delphi side all from a simple API.

## Downloads
<a href="https://github.com/tinyBigGAMES/CPas/releases" target="_blank">**Releases**</a> - These are the official release versions.

## Features
- **Free** for commercial use. See <a href="https://github.com/tinyBigGAMES/CPas/blob/main/LICENSE" target="_blank">License agreement</a>.
- Allow C integration with <a href="https://www.embarcadero.com/products/Delphi" target="_blank">Delphi</a> and <a href="https://www.freepascal.org/" target="_blank">FreePascal</a> at run-time.
- Support Windows 32/64-bit target platforms.
- Support for C99.
- Fast run-time compilation.
- Can run C sources directly or compile to (**.LIB**, **.EXE**, **.DLL**).
- Library files can be loaded and used at run-time from a file, a resource or stream.
- Import symbols directly from a dynamic linked library (**.DLL**) or module-definition (**.DEF**) file.
- You can reference the symbols from Pascal and directly access their value (mapping to a routine and data).
- Your application can dynamically or statically link to CPas.
- Direct access to the vast quantity of C99 libraries inside Delphi.
- Project directives to control project settings at compile-time.
- Your application can link to CPas dynamically or statically.

## Minimum System Requirements
- Delphi 10 (Win32/Win64 targets only)
- FreePascal 3.3.3 (Win32/Win64 targets only)
- Microsoft Windows 10, 64-bits
- 20MB of free hard drive space

## How to use in Delphi
- Unzip the archive to a desired location.
- Add `installdir\sources`, folder to Delphi's library path so the CPas binding files can be found for any project or for a specific project add to its search path.
- Add `installdir\bin`, folder to Windows path so that CPas DLLs can be found for any project or place beside project executable.
- See examples in `installdir\examples` for more information about usage.
- You must include CPas DLLs (`CPas32.dll` or `CPas64.dll`) in your project distribution when dynamically linked to CPas.
- See `installdir\help` for documentation.

**NOTE:** For your assurance and peace of mind, all official executables in the CPas distro that were created by us are code signed by **tinyBigGAMES LLC**. 

## A Tour of CPas
### CPas API
You access the easy to use API in Delphi from the `CPas` unit.
```pascal

type
  { TCPas }
  TCPas = type Pointer;

  { TCPasOutput }
  TCPasOutput = (cpMemory, cpLib, cpEXE, cpDLL);

  { TCPasExe }
  TCPasExe = (cpConsole, cpGUI);

  { TCPasErrorMessageEvent }
  TCPasErrorEvent = procedure(aSender: Pointer; const aMsg: WideString);

{ Misc }
function  cpVersion: WideString;

{ Context management }
function  cpNew: TCPas;
procedure cpFree(var aCPas: TCPas);
procedure cpReset(aCPas: TCPas);

{ Error handling }
procedure cpSetErrorHandler(aCPas: TCPas; aSender: Pointer; aHandler: TCPasErrorEvent);
procedure cpGetErrorHandler(aCPas: TCPas; var aSender: Pointer; var aHandler: TCPasErrorEvent);

{ Preprocessing }
procedure cpDefineSymbol(aCPas: TCPas; const aName: WideString; const aValue: WideString);
procedure cpUndefineSymbol(aCPas: TCPas; const aName: WideString);
function  cpAddIncludePath(aCPas: TCPas; const aPath: WideString): Boolean;
function  cpAddLibraryPath(aCPas: TCPas; const aPath: WideString): Boolean;

{ Compiling }
procedure cpSetOuput(aCPas: TCPas; aOutput: TCPasOutput);
function  cpGetOutput(aCPas: TCPas): TCPasOutput;
procedure cpSetExe(aCPas: TCPas; aExe: TCPasExe);
function  cpGetExe(aCPas: TCPas): TCPasExe;
function  cpAddLibrary(aCPas: TCPas; const aName: WideString): Boolean;
function  cpAddFile(aCPas: TCPas; const aFilename: WideString): Boolean;
function  cpCompileString(aCPas: TCPas; const aBuffer: string): Boolean;
procedure cpAddSymbol(aCPas: TCPas; const aName: WideString; aValue: Pointer);
function  cpLoadLibFromFile(aCPas: TCPas; const aFilename: WideString): Boolean;
function  cpLoadLibFromResource(aCPas: TCPas;  aInstance: THandle; const aResName: WideString): Boolean;
function  cpLoadLibFromMemory(aCPas: TCPas; const aBuffer: Pointer; const aSize: Int64): Boolean;
function  cpSaveOutputFile(aCPas: TCPas; const aFilename: WideString): Boolean; 
function  cpRelocate(aCPas: TCPas): Boolean;
function  cpRun(aCPas: TCPas): Boolean;
function  cpGetSymbol(aCPas: TCPas; const aName: WideString): Pointer;
function  cpCompile(aCPas: TCPas; const aFilename: WideString): Boolean;

{ Stats }
procedure cpStartStats(aCPas: TCPas);
function  cpEndStats(aCPas: TCPas; aShow: Boolean): WideString;

{ Resources }
procedure cpSetExeIcon(aCPas: TCPas; const aFilename: WideString);
function  cpGetExeIcon(aCPas: TCPas): WideString;
procedure cpSetAddVersionInfo(aCPas: TCPas; aAddVersionInfo: Boolean);
function  cpGetAddVersionInfo(aCPas: TCPas): Boolean;
procedure cpSetVersionInfo(aCPas: TCPas; const aCompanyName: WideString;
  const aFileVersion: WideString; const aFileDescription: WideString;
  const aOriginalFilename: WideString; const aLegalCopyright: WideString;
  const aComments: WideString);
procedure cpGetVersionInfo(aCPas: TCPas; var aCompanyName: WideString;
  var aFileVersion: WideString; var aFileDescription: WideString;
  var aOriginalFilename: WideString; var aLegalCopyright: WideString;
  var aComments: WideString);
```
### Linking to CPas
Your applcation can link dynamiclly or statically to CPas. For dynamic linking (which require you to include either **CPas32.dll** or **CPas64.dll** with your distro), simply add `CPas` to your projects uses section. For static linking (which does not require any an external DLL), instead use `CPas.Static`. You can **NOT** have both enabled at the same time, your application will gracefully terminate with an warning message.

### Project Directives
Directives added to your source file and compiled via `cpCompile`, will allow you to control project settings at compile time. You add them via a comment block at the top of your main project source file. Quotes surrounding the values are optional, but necessory for values with spaces as seen below.
```C
/* === PROJECT DIRECTIVES ===
@SetOutput        "EXE"
@SetExe           "Console"
@SetOutputname    "output/MyCompileFile"
@AddVersionInfo   "YES"  
@CompanyName      "tinyBigGAMES(tm) LLC" 
@FileVersion      "1.0.0"
@FileDescription  "MyCompileFile"
@OriginalFilename "MyCompileFile.exe"
@LegalCopyright   "Copyright (c) 2022 tinyBigGAMES(tm) LLC"
@Comments         "https://tinybiggames.com"
*/

#include <stdio.h>

void main(void)
{
  printf("Hello World!\n");  
}

```

CPas supports the following project directives:

| DIRECTIVE         | VALUES               | DISCRIPTION             |
|-------------------|----------------------|-------------------------|
| @SetOutput        | EXE, DLL, LIB        | Set compile module type |
| @SetExe           | CONSOLE, GUI         | Set EXE subsystem |
| @SetOutputname    | name                 | Module output filename |
| @AddIncludePath   | valid path           | C include file path |
| @AddLibraryPath   | valid path           | Library location in filesystem |
| @AddLibrary       | library name         | Library name (no extenstion) |
| @AddFile          | .C, .LIB, .DEF, .DLL | Add file to compile or to reference |
| @AddVersionInfo   | YES, NO, TRUE, FALSE | Enable/disable adding version info |
| @CompanyName      | company name         | File company name |
| @FileVersion      | SemVer               | File version in major.minor.path format |
| @FileDescription  | description          | File description |
| @OriginalFilename | filename             | Filename |
| @LegalCopyright   | copyright            | File copyright |
| @Comments         | comments             | File comments |

### How to use
A minimal implementation example:
```pascal
uses
  System.SysUtils,
  CPas; //<--- use for dynamic linking
  //CPas.Static; //<--- use for static linking

var
  c: TCPas;
  
// CPas error handler
procedure ErrorHandler(aSender: Pointer; const aMsg: WideString);
begin
  WriteLn(aMsg);
end;  
  
begin
  // create a CPas instance
  c := cpNew;
  try
    // setup the error handler
    cpSetErrorHandler(c, nil, ErrorHandler);
    
    // add source file
    cpAddFile(cp, 'test1.c');

    // link and call main
    cpRun(cp);
  finally
    // destroy CPas instance
    cpFree(c);
  end;
end.
```
See the examples for more information on usage.

## Compatibility
A curated <a href="https://github.com/tinyBigGAMES/cpLibs" target="_blank">repo</a> of compatible libraries for CPas.

## Media

https://user-images.githubusercontent.com/69952438/156104143-bffb6c25-7bfa-4697-8413-4ac1740323cd.mp4


https://user-images.githubusercontent.com/69952438/156843415-f6566612-e7d8-41d6-bc3a-a76977cb95ee.mp4


## Support

| DESCRIPTION  | URL |
|-|-|
|Project Discussions| https://github.com/tinyBigGAMES/CPas/discussions |
| Project Tracking | https://github.com/tinyBigGAMES/CPas/projects |
| Website | https://tinybiggames.com |
| E-Mail | mailto:support@tinybiggames.com |
| Discord | https://discord.gg/tPWjMwK |
| Twitter | https://twitter.com/tinyBigGAMES |
| Facebook | https://facebook.com/tinyBigGAMES |
| YouTube | https://youtube.com/tinyBigGAMES |

## Sponsor
If this project has been useful to you, please consider sponsoring to help with it's continued development. **Thank You!** :clap:

<a href="https://www.buymeacoffee.com/tinybiggames"><img src="https://img.buymeacoffee.com/button-api/?text=Sponsor this project&emoji=&slug=tinybiggames&button_colour=FFDD00&font_colour=000000&font_family=Cookie&outline_colour=000000&coffee_colour=ffffff" /></a>

<p align="center">
 <a href="https://www.embarcadero.com/products/delphi" target="_blank"><img src="media/delphi.png"></a><br/>
 <b>❤ Made in Delphi</b>
</p>

