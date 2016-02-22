# Version Guidelines

This document provides guidelines for EDK II Package Maintainers and Module 
Developers. Specifically aimed at when and why the spec version, GUID and file
version values should be modified.

Refer to the *UEFI Platform Initializat Distribution Packaging Specfication*
for description of Package and Module Surface Area Descriptions.

* http://www.uefi.org/specifications


GUIDs and versions in the EDK II INF and DEC meta-data files identify the 
Surface Area Descriptions of EDK II Packages and Modules at a given point in
time.


## Rationale

GUIDs and versions discussed in the document may be used by consumers of an 
EDK II package to identify changes to packages that may impact their own 
development.

These values are used by tools that create and install UEFI Distribution 
Packages (UDP) conforming to the *UEFI Platform Initialization Distribution 
Packaging Specification*.

Other tools may use these values to determine if the INF/DEC files can be 
processed or whether other content (declarations, library instances or 
modules) is still available.

Some tools may use the surface area descriptions for checking design rules.


**Always check the released versions of the EDK II Specifications**
* https://github.com/tianocore/Docs

***Note:*** *Bug fixes to modules do not require changes to version values
provided no features were added.*


---

i. [DEC File Versioning](edk2_dec_files.md)
 
ii. [INF File Versioning](edk2_inf_files.md)


