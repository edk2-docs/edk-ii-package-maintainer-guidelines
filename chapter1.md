# Version Guidelines

This chapter provides guidelines for both the Package Maintainer and Module Developer. Specifically aimed at when and why the spec version, GUID and file version values should be modified.

**Always check the released versions of the EDK II Specification**

* https://github.com/tianocore/Docs

**Note:** *Bug fixes to modules do not require changes to version values.*


## EDK II Package Declaration (DEC) Files
**SPECIFICATION:** *EDK II Package Declaration (DEC) File Specification*

### DEC_SPECIFICATION
1. New EDK II Packages shall always use the value specified in the current version of the DEC spec.
2. When the Package Maintainer adds content not defined in the spec that was current at the time the DEC file was created, the value shall be updated to the value specified in the current version of the DEC spec.
3. The TianoCore wiki documents are written generically (and are not maintained). As such, these pages may have incorrect versions of the ```DEC_SPECIFICATION``` values.

**Rationale**

Tools that process the EDK II Meta-data files may use this value to determine whether the tool can process all information in the file.
- Some tools may choose to provide warning messages, while other tools may give error messages.
- Some tools may choose to examine content that was defined at the time of the spec release, and ignore content that was introduced in later versions of the specification.

### PACKAGE_GUID values
This value shall be changed when a non-backward compatible change is made to the DEC file or content declared in the DEC has been modified.

**Rationale**

This value is used by tools that create and install UEFI Distribution Packages (http://www.uefi.org/specifications).

Other tools may use the GUID value (along with the ```PACKAGE_VERSION```) to determine whether non-backward compatible changes have been made to the package. This may also be used by design rule checking tools.

Non-backward compatible changes may cause build errors, when a module in a different packages uses content declared in another EDK II package that is no longer available.

**Non-backward compatible changes include, but are not limited to the following:**

* Library Classes
    * Removal of a Library Class (including the header file)
    * Modifying a data structure in a library class header file by removing, reordering or changing a data type
* GUIDs
    * Removal of a GUID Declaration
    * Modifying a data structure in a GUID's header file by removing, reordering or changing a data type
* Protocols
    * Removal of a Protocol Declaration
    * Modifying a data structure in a Protocol's header file by removing, reordering or changing a data type
* PPIs
    * Removal of a PPI Declaration
    * Modifying a data structure in a PPI's header file by removing, reordering or changing a data type
*PCDs
    * Removal of a PCD Declaration
    * Redefinition of a PCD's Access Method (changing a FixedAtBuild PCD to a FeatureFlag PCD)
    * Changing the Token Number, Datum Type or TokenSpaceGuidCName in a PCD entry.

### PACKAGE_VERSION values
The value consists of a major number and a minor number.

#### Major Number
1. If the PACKAGE_GUID value changes, the major number may be reset to a starting value.
2. If the PACKAGE_GUID value is unchanged and new content is added due to new UEFI/PI Specification releases, the major number may be incremented.
3. If the PACKAGE_GUID value is unchanged and new comment is added due to other Industry Standard Specification releases, the major number may be incremented.

#### Minor Number
1. If the PACKAGE_GUID value changes, the minor number may be reset to a starting value.
2. If the PACKAGE_GUID value is unchanged and new content is added (not a result of an update to any specification), the minor number may be incremented.


**Rationale**

This value is used by tools that create and install UEFI Distribution Packages (http://www.uefi.org/specifications).

Other tools may use this value to determine if new content has been added to the DEC file.

New content is define as:
* Adding a new library class
* Adding a new GUID
* Adding a new Protocol
* Adding a new PPI
* Adding a new PCD
* 


## EDK II Module Information (INF) Files

**SPECIFICATION:** *EDK II Module Information (INF) File Specification*

### INF_VERSION
Unfortunately, the name of this entry is a bit misleading (sorry about that). This entry represents the version of the INF specification, not the version of the INF.

1. New EDK II Modules shall always use the value specified in the current version of the INF spec.
2. When the Module Developer adds content not defined in the spec that was current at the time the INF file was created, the value shall be updated to the value specified in the current version of the INF spec.
3. The TianoCore wiki documents are written generically (and are not maintained). As such, these pages may have incorrect versions of the ```INF_VERSION``` values.

### FILE_GUID
This value shall be changed when a non-backward compatible change is made to the INF file from a change to the module's code.

**Rationale**

This value is used by tools that create and install UEFI Distribution Packages (http://www.uefi.org/specifications).

Other tools may use the GUID value (along with the ```VERSION_STRING```) to determine whether non-backward compatible changes have been made to the module. This may also be used by design rule checking tools.

Non-backward compatible changes may cause build errors, when a module no longer produces a GUID, PROTOCOL or PPI that was produced in a previous version of the module.

**Non-backward compatible changes include, but are not limited to the following:**
1. A GUID is no longer produced
2. A PROTOCOL is no longer producted
3. A PPI is no longer producted
4. A PCD's access method was changed in the code, such as using PcdGetEx instead of PcdGet macros
5. A PCD's access method was changed due to a change in the DEC file that declared the PCD
 

