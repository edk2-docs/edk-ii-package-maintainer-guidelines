# Version Guidelines

This chapter provides guidelines for both the Package Maintainer and Module Developer. Specifically aimed at when and why the spec version, GUID and file version values should be modified.

**Rationale**

GUIDs and versions discussed in the document may be used by consumers of an EDK II package to identifiy changes to packages that may impact their own development.

These values are used by tools that create and install UEFI Distribution Packages (UDP) conforming to the *UEFI Platform Initialization Distribution Packaging Specification*.
* http://www.uefi.org/specifications

Other tools may use these values to determine if the INF/DEC files can be processed or whether other content (declarations, library instances or modules) is still available.

**Always check the released versions of the EDK II Specifications**
* https://github.com/tianocore/Docs

***Note:*** *Bug fixes to modules do not require changes to version values provided no features were added.*


## EDK II Package Declaration (DEC) Files
**SPECIFICATION:** *EDK II Package Declaration (DEC) File Specification*

### DEC_SPECIFICATION value
1. New EDK II Packages shall always use the value specified in the current version of the DEC spec.
2. When the Package Maintainer adds content not defined in the spec that was current at the time the DEC file was created, the value shall be updated to the value specified in the current version of the DEC spec.
3. The TianoCore wiki documents are written generically (and may not be updated every time a specification is changed). As such, these pages may have incorrect versions of the ```DEC_SPECIFICATION``` values.

**Rationale**

Tools that process the EDK II Meta-data files may use this value to determine whether the tool can process all information in the file.
* Some tools may choose to provide warning messages, while other tools may give error messages.
* Some tools may choose to examine content that was defined at the time of the spec release, and ignore content that was introduced in later versions of the specification.

### PACKAGE_GUID value
This value shall be changed when a non-backward compatible change is made to the DEC file or content declared in the DEC has been modified.

There are many tools available to create new GUID values. There is a Web site where a GUID can be generated: http://www.guidgen.com. Microsoft Visual Studio also has a GUID generator. Linux distributions may also come with a GUID generator, such as uuid.

Package Maintainers may update the GUID value if there are significant new features added to a package that are not related to any new specs instead of updating the ```PACKAGE_VERSION``` value.

**Rationale**

Tools may use the GUID value (along with the ```PACKAGE_VERSION```) to determine whether non-backward compatible changes have been made to the package. This may also be used by design rule checking tools.

Non-backward compatible changes may cause build errors, when a module in a different packages uses content declared in another EDK II package that is no longer available.


**Non-backward compatible changes include, but are not limited to the following:**

* Library Classes
    - Removal of a Library Class (including the header file)
    - Modifying a data structure in a library class header file by removing, reordering or changing a data type
* GUIDs
    - Removal of a GUID Declaration (including the header file)
    - Modifying a data structure in a GUID's header file by removing, reordering or changing a data type
    - An API is removed or modified in a non-backward compatible way
* PROTOCOLs
    - Removal of a PROTOCOL Declaration (including the header file)
    - Modifying a data structure in a Protocol's header file by removing, reordering or changing a data type
    - An API is removed or modified in a non-backward compatible way
* PPIs
    - Removal of a PPI Declaration (including the header file)
    - Modifying a data structure in a PPI's header file by removing, reordering or changing a data type
    - An API is removed or modified in a non-backward compatible way
* PCDs
    - Removal of a PCD Declaration
    - Deleting of a PCD's Access Method (i.e., changing a **FixedAtBuild** PCD to a **FeatureFlag** PCD)
    - Changing the Token Number, Datum Type or Token Space GUID C Name in a PCD entry.
    - Adding restrictions to the validation tags (i.e., removing a value from a ```@ValidList``` entry)
* Modules
    - Modules Removed from a Package (Library Class Instances and other modules)

** Examples of backward compatible changes include, but are not limited to the following:**
* Library Classes
    *  Adding a new library class
    *  Adding a new data structure to a library class header
* GUIDs
    *  Adding a new GUID declaration
    *  Adding a new API to the GUID's header
* PROTOCOLS
    * Adding a new PROTOCOL declaration
    * Adding a new API to the protocol's header
* PPIs
    * Adding a new PPI declaration
    * Adding a new API to the PPI's header
* PCDs
    * Adding a new PCD declaration
    * Modifying the default value of the PCD
    * Updating the ```@PROMPT``` or ```HELP``` strings
    * Allow a PCD to use additional Access Methods (adding **FixedAtBuild** PCD to **PatchableInModule** PCD access methods)
* Modules
    * Adding new modules (Package Maintainer may optionally update the GUID)

### PACKAGE_VERSION value
The version number is used to track backward compatible changes to an EDK II package. The value should increment when new features are added, however, there are no hard and fast rules about the ```PACKAGE_VERSION``` value. 

The value consists of a major number and a minor number. 

When the GUID value (above) changes, the package maintainer may choose to do one of the following:
1. Increment the value, say from 1.10 to 2.0, indicative of a new release of this package. 
2. Reset the value to 1.0, indicative of the first version of this package identified by this GUID.
3. Leave the value untouched, for example if the the current version is 1.0

#### Major Number
The following are recommended practices:
1. If the ```PACKAGE_GUID``` value changes, the major number may be reset to a starting value or it may be incremented.
2. If the ```PACKAGE_GUID``` value is unchanged and new content is added due to new UEFI/PI Specification releases, the major number should be incremented.
3. If the ```PACKAGE_GUID``` value is unchanged and new content is added due to other Industry Standard Specification releases, the major number should be incremented.

#### Minor Number
The following are recommended practices:
1. If the ```PACKAGE_GUID``` value changes, the minor number may be reset to a starting value, such as 0, if the major number was incremented or reset to a starting value.
2. The minor number should be incremented if the ```PACKAGE_GUID``` value is unchanged and new content is added (not a result of an update to any specification), and the major number was not incremented. This includes adding content to the ```PACKAGE_UNI_FILE``` or adding comment block content (like ```@PROMPT``` or ```@ValidList``` entries).
3. If new modules are added to the package and these modules are not covered by previous rules to GUID, major or minor number changes, the minor number shall be incremented.

**Rationale**

Tools may use this value to determine if new content has been added to the DEC file  EDK II's UEFI Packaging Tool, UEFIPT, provided with the EDK II BaseTools, uses this value during UDP

New content is define as:
* Adding a new library class
* Adding a new GUID
* Adding a new PROTOCOL
* Adding a new PPI
* Adding a new PCD
* Adding new values to a ```@ValidList```


## EDK II Module Information (INF) Files

**SPECIFICATION:** *EDK II Module Information (INF) File Specification*

### INF_VERSION value
Unfortunately, the name of this entry is a bit misleading. This entry represents the version of the INF specification, not the version of the INF.

1. New EDK II Modules shall always use the value specified in the current version of the INF spec.
2. When the Module Developer adds content not defined in the spec that was current at the time the INF file was created, the value shall be updated to the value specified in the current version of the INF spec.
3. The TianoCore wiki documents are written generically (and may not be updated every time a specification is changed). As such, these pages may have incorrect versions of the ```INF_VERSION``` values.

### FILE_GUID value
This value shall be changed when a non-backward compatible change is made to the INF file from a change to the module's code.

There are many tools available to create new GUID values. There is a Web site where a GUID can be generated:  http://www.guidgen.com.  Microsoft Visual Studio also has a GUID generator. Linux distributions may also come with a GUID generator, such as uuid.

**Rationale**

Tools may use the ```FILE_GUID``` value (along with the ```VERSION_STRING```) to determine whether non-backward compatible changes have been made to the module. This may also be used by design rule checking tools.

Non-backward compatible changes may cause build errors, when a module no longer produces a GUID, PROTOCOL or PPI that was produced in a previous version of the module.

**Non-backward compatible changes include, but are not limited to the following:**

* A GUID is no longer produced
* A PROTOCOL is no longer produced
* A PPI is no longer produced
* Changing a PROTOCOL, PPI or GUID's USAGE from ```CONSUMES``` to ```PRODUCES```
* A PCD's access method was changed in the code, such as using ```PcdGetEx``` instead of ```PcdGet``` macros
* A PCD's access method was changed due to a change in the DEC file that declared the PCD
* A PCD from one package is replaced by a PCD from another EDK II package
* Adding or changing entries to a DEPEX expression
 

**Examples of backward compatible changes include, but are not limited to the following:**
* Removing a Library Class dependency
* Changing a ```SOMETIMES_PRODUCES``` or ```SOMETIMES_CONSUMES``` to ```PRODUCES``` or ```CONSUMES```
* Removing entries from the DEPEX expression
* Adding additional .C or .UNI files to a module (such as splitting a single .C file into .C and .H files)
* Removing a GUID, PROTOCOL or PPI that had a ```USAGE``` of ```CONSUMES``` or ```SOMETIMES_CONSUMES```

 
### VERSION_STRING value
The value consists of a major number and a minor number.

#### Major Number
1. If the ```FILE_GUID``` value changes, the major number may be reset to a starting value, such as 1, or it may be incremented.
2. If the ```FILE_GUID``` value is unchanged and new functionality is added due to new UEFI/PI Specification releases, the major number shall be incremented.
3. If the ```FILE_GUID``` value is unchanged and new functionality is added due to other Industry Standard Specification releases, the major number shall be incremented.

#### Minor Number
1. If the ```FILE_GUID``` value changes, the minor number shall be reset to a starting value.
2. If the ```FILE_GUID``` value is unchanged and new functionality is added (not a result of an update to any specification), the minor number shall be incremented. 
3. If the ```FILE_GUID``` is unchanged and content is added to the ```MODULE_UNI_FILE``` file or adding comment block content (like adding ```# USAGE``` entries), the minor number may be incremented.


**Rationale**

Tools may use this value to determine if new functionality has been added to the module.

New functionality is define as:
* Requiring a new library class for the module to function
* Consuming or producing a new GUID
* Consuming or producing a new Protocol
* Consuming or producing a new PPI
* Adding support for another module type
* Using a new PCD
