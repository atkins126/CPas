# CHANGELOG :: CPas-C for Delphi
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
