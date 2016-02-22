# Surface Area Definitions

## Package Surface Area

A complete description of the elements a package provides to support building
modules. This includes header files for industry standard specifications, 
library header files, include file paths within the package, GUID declarations, 
PPI declarations, Protocol declarations, and Platform Configuration Database 
element declarations. All of these package elements are available to Module 
Developers and can be used to describe the Module Surface Area of a module.

## Module Surface Area

A full description of all of the elements a module produces and/or consumes 
that allow it to be integrated into a platform firmware image and executed as 
expected. These elements include binary file names, source file names, 
packages, libraries, protocols, PPIs, GUIDs, events, Platform Configuration
Database elements, UEFI variables, UEFI System Configuration Tables, boot 
modes, HOBs, HII packages, and external variable and function names 
(including the module's entry point).

Binary modules must minimally describe the dependencies required for a the 
module to execute correctly. Source modules must minimally describe their 
dependencies so that it can be compiled and linked into a binary module.

Modules may also have run-time dependencies that must be satisfied in order 
for the module to execute correctly.