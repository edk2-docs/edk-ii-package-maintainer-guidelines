# Version Guidelines

This document provides guidelines for both the Package Maintainer and Module 
Developer. Specifically aimed at when and why the spec version, GUID and file
version values should be modified.

Refer to the *UEFI Platform Initializat Distribution Packaging Specfication*
for description of Package and Module Surface Area Descriptions.

* http://www.uefi.org/specifications


GUIDs and versions in the EDK II INF and DEC meta-data files identify the 
Surface Area Descriptions of EDK II Packages and Modules at a given point in
time.

## Surface Area Definitions

### Package Surface Area

A complete description of the elements a package provides to support building
modules. This includes header files for industry standard specifications, 
library header files, include file paths within the package, GUID declarations, 
PPI declarations, Protocol declarations, and Platform Configuration Database 
element declarations. All of these package elements are available to Module 
Developers and can be used to describe the Module Surface Area of a module.

### Module Surface Area

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

## Rationale

GUIDs and versions discussed in the document may be used by consumers of an 
EDK II package to identifiy changes to packages that may impact their own 
development.

These values are used by tools that create and install UEFI Distribution 
Packages (UDP) conforming to the *UEFI Platform Initialization Distribution 
Packaging Specification*.

Other tools may use these values to determine if the INF/DEC files can be 
processed or whether other content (declarations, library instances or 
modules) is still available.

**Always check the released versions of the EDK II Specifications**
* https://github.com/tianocore/Docs

***Note:*** *Bug fixes to modules do not require changes to version values
provided no features were added.*


---

i. [DEC File Versioning](edk2_dec_files.md)
 
ii. [INF File Versioning](edk2_inf_files.md)


