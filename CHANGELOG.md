# CHANGELOG :: CPas-C for Delphi
## Version 1.3.stable
- Reworked all examples to support 32/64-bits
- Update cpLoadLibFromResource to include an instance (THandle) parameter
- Added a runtime check to make sure CPas and CPas.Static are not used simultaneously
- FPC can now build static releases also
- Add CPas.Static unit now for static builds
- Reformated CHM help format
- Added cpCompile with project directives support
- Replaced cpLoadLibFromStream with cpLoadLibFromMemory
- Refactored codebase and added 32-bit support :sunglasses:
- Updated cpAddLibrary to support (.LIB) files
- Updated cpSetVerionInfo to validate FileVersion as SemVer format (major.minor.patch)
- Miscellaneous fixes and enhancements
## Version 1.2.stable
- Added updated existing examples to use new/updates functions
- Added cpGetVersionInfo, get version information
- Added cpSetVersionInfo, set version information
- Added cpGetAddVersionInfo, get add version info
- Added cpSetAddVersionInfo, set add version info
- Added cpGetExeIcon, get EXE icon filename
- Added cpSetExeIcon, set EXE icon filename
- Miscellaneous enhancements
## Version 1.1.stable
- Added output_exe example
- Added ouput_dll example
- Added updated existing examples to use new/updates functions
- Added cpSetExe, set the EXE subsystem type
- Added cpGetExe, return the EXE subsystem type
- Added cpGetOutput, return output type
- Added TCPasExe (cpConsole, cpGUI) enum
- Added cpAddLibrary
- Added cpEXE, cpDLL to TCPasOutput enum
- Renamed cpSaveLibToFile to cpSaveOutputFile
- CPas can now output .LIB, .EXE and .DLL files
- Renamed cpLink to cpRelocate
- Patched CPas.pas to work with FreePascal (ppcx64)

## Version 1.0.stable
- Added add_symbol example
- Added compile_string example
- Added cpCompileString to compile a string containing a C source
- Added cpAddSymbol to add a symbol to the compiled program
- Added cpStartStats & cpEndStats to show compilation stats 
## Version 1.0.alpha1
- Initial release 
