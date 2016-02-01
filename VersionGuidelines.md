# Version Guidelines

This document provides guidelines for both the Package Maintainer and Module 
Developer. Specifically aimed at when and why the spec version, GUID and file
version values should be modified.

**Rationale**

GUIDs and versions in the EDK II INF and DEC meta-data files identify the 
Surface Area Descriptions of EDK II Packages and Modules at a given point in
time.

GUIDs and versions discussed in the document may be used by consumers of an 
EDK II package to identifiy changes to packages that may impact their own 
development.

These values are used by tools that create and install UEFI Distribution 
Packages (UDP) conforming to the *UEFI Platform Initialization Distribution 
Packaging Specification*.

* http://www.uefi.org/specifications

Other tools may use these values to determine if the INF/DEC files can be 
processed or whether other content (declarations, library instances or 
modules) is still available.

**Always check the released versions of the EDK II Specifications**
* https://github.com/tianocore/Docs

***Note:*** *Bug fixes to modules do not require changes to version values
provided no features were added.*


[DEC File Versioning](edk2_dec_files.md)

[INF File Versioning](edk2_inf_files.md)


