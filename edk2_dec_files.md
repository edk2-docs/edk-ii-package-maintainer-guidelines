# EDK II Package Declaration (DEC) Files

**SPECIFICATION:** *EDK II Package Declaration (DEC) File Specification*

## DEC_SPECIFICATION value
1. New EDK II Packages shall use the value specified in the current version
of the DEC spec.
2. When the Package Maintainer adds content not defined in the spec that was
current at the time the DEC file was created, the value shall be updated to 
the value specified in the current version of the DEC spec.
3. The TianoCore wiki documents are written generically (and may not be  
updated every time a specification is changed). As such, the wiki pages may 
have incorrect versions of the ```DEC_SPECIFICATION``` values.

**Rationale**

Tools that process the EDK II Meta-data files may use this value to determine 
whether the tool can process all information in the file.
* Some tools may choose to provide warning messages, while other tools may 
give error messages.
* Some tools may choose to examine content that was defined at the time of the
spec release, and ignore content that was introduced in later versions of the 
specification.

## PACKAGE_GUID value

The ```PACKAGE_GUID``` value identifies the Package Surface Area at a given 
point in time.

This value shall be changed when a non-backward compatible change is made to 
the DEC file or content declared in the DEC has been modified.

There are many tools available to create new GUID values. There is a Web site 
where a GUID can be generated: http://www.guidgen.com. Microsoft Visual Studio 
also has a GUID generator, uuidgen. Linux distributions may also come with a 
GUID generator, such as uuid.

Package Maintainers may update the GUID value if there are significant new 
features added to a package that are not related to any new specs instead of 
updating the ```PACKAGE_VERSION``` value.

**Rationale**

Tools may use the GUID value (along with the ```PACKAGE_VERSION```) to 
determine whether non-backward compatible changes have been made to the package.
This may also be used by design rule checking tools.

Non-backward compatible changes may cause build errors, when a module in a 
different packages uses content declared in another EDK II package that is no
longer available.


### Library Classes
    
* **A GUID change is required for non-backward compatible changes** including,
but not limited to the following:
    - Removal of a Library Class (including the header file)
    - Modifying a data structure in a library class header file by removing, 
    reordering or changing a data type
* **A GUID change is not necessary for backward comapatible changes*** including,
but not limited to the following:
    -  Adding a new library class
    -  Adding a new function to a library class
    -  Adding a new data structure to a library class header
    -  Extending or adding new functions or members

### GUIDs

* **A GUID change is required for non-backward compatible changes** including,
but not limited to the following:
    - Removal of a GUID Declaration (including the header file if applicable)
    - Modifying a data structure in a GUID's header file by removing, reordering 
    or changing a data type
    - An API is removed or modified in a non-backward compatible way
* **A GUID change is not necessary for backward comapatible changes*** including,
but not limited to the following:
    -  Adding a new GUID declaration
    -  Adding a new API to the GUID's header (if applicable)
    -  Extending or adding new functions or members

### PROTOCOLs

* **A GUID change is required for non-backward compatible changes** including,
but not limited to the following:
    - Removal of a PROTOCOL Declaration (including the header file)
    - Modifying a data structure in a Protocol's header file by removing,
    reordering or changing a data type
    - An API is removed or modified in a non-backward compatible way
* **A GUID change is not necessary for backward comapatible changes*** including,
but not limited to the following:
    - Adding a new PROTOCOL declaration
    - Adding a new field to the protocol's header
    - Extending or adding new functions or member

### PPIs

* **A GUID change is required for non-backward compatible changes** including,
but not limited to the following:
    - Removal of a PPI Declaration (including the header file)
    - Modifying a data structure in a PPI's header file by removing, reordering
    or changing a data type
    - An API is removed or modified in a non-backward compatible way
* **A GUID change is not necessary for backward comapatible changes*** including,
but not limited to the following:
    * Adding a new PPI declaration
    * Adding a new field to the PPI's header
    * Extending or adding new functions or members

### PCDs

* **A GUID change is required for non-backward compatible changes** including,
but not limited to the following:
    - Removal of a PCD Declaration
    - Removing or changing of a PCD's Access Method (i.e., changing a 
    **FixedAtBuild** PCD to a **FeatureFlag** PCD)
    - Changing the Token Number, Datum Type or Token Space GUID C Name in a
    PCD entry.
    - Adding restrictions to the validation tags (i.e., removing a value 
    from a ```@ValidList``` entry)
* **A GUID change is not necessary for backward comapatible changes*** including,
but not limited to the following:
    - Adding a new PCD declaration
    - Reordering the PCDs within an Access Method section
    - Modifying the default value of the PCD
    - Updating the ```@PROMPT``` or ```HELP``` strings
    - Allow a PCD to use additional Access Methods (adding **FixedAtBuild** PCD
    to **PatchableInModule** PCD access methods)

### Modules

* **A GUID change is required for non-backward compatible changes** including,
but not limited to the following:
    - Modules Removed from a Package (Library Class Instances and other modules)
* **A GUID change is not necessary for backward comapatible changes*** including,
but not limited to the following:
    - Adding new modules (Package Maintainer may optionally update the GUID)

## PACKAGE_VERSION value

The version number is used to track backward compatible changes to an EDK II 
package. The value should increment when new features are added however, there
are no hard and fast rules about updating the ```PACKAGE_VERSION``` value. 

**Rationale**

Tools may use this value to determine if new content has been added to the DEC
file.

For example, EDK II's UEFI Packaging Tool, UEFIPT, provided with the EDK II 
BaseTools, uses this value during UDP creation. During installation, UEFIPT 
uses these values to follow dependency rules defined by the UDP spec.

The value consists of a major number and an optional minor number. Best 
practices suggest using both a major and minor number.


## Best Practices
The following are recommended practices:

* When the ```PACKAGE_GUID``` is changed:
    - Increment the major number and reset the minor number to 0, i.e.,
    1.10 to 2.0.
    

* When the ```PACKAGE_GUID``` is not changed:
    - If new content is added due to new UEFI/PI Specification releases,
    increment the major number and reset the minor number to 0.
    - If new content is added due to other Industry Standard Specification
    releases, increment the major number and reset the minor number to 0.
    - If a significant number of modules is added, increment the major
    number and reset the minor number to 0.
    - If the package maintainer wants to ```tag``` a package for any other
    reason, increment the major number and reset the minor number to 0.
 

* When the ```PACKAGE_GUID``` and major number are not changed:
    - Increment the minor number if new modules are added (not a result of
    an update to any specification).
    - Increment the minor number if content is added (see below).      
    - If new modules are added to the package and these modules are not
    covered by previous recommendations, increment the minor number.

New content implies a change to the Description of a Package Surface Area
(see the UDP spec).

* **Examples of new content** include, but are not limited to the following:
  - Adding meta-tags (```@PROMPT``` or ```@ValidList``` comment block
  entries) that map to attributes or elements defined by the UDP
  specification
  - Adding new entries in the (```PACKAGE_UNI_FILE```) that maps to elements
  defined by the UDP specification, such as adding new PROMPT strings
  associated with a new PCD
  - Adding a new library class
  - Adding a new GUID
  - Adding a new PROTOCOL
  - Adding a new PPI
  - Adding a new PCD
  - Adding new values to a ```@ValidList```


* **Examples of content changes where the major and minor number do not
need to be changed** include, but are not limited to the following:
    - Bug fixes in code
    - Spelling changes in comment content
    - Adding more help text before GUID, PROTOCOL, PPI or PCD entries.
    - Adding new language translations of existing entries in the 
    ```PACKAGE_UNI_FILE```

