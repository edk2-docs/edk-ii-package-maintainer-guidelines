# EDK II Module Information (INF) Files

**SPECIFICATION:** *EDK II Module Information (INF) File Specification*

Module developers may change ```FILE_GUID``` or ```VERSION_STRING``` values
at any time.

## INF_VERSION value

Unfortunately, the name of this entry is a bit misleading. This entry 
represents the version of the INF specification, not the version of the 
INF file.


1. New EDK II Modules shall always use the value specified in the current 
version of the INF spec.
2. When the Module Developer adds content not defined in the spec that was
current at the time the INF file was created, the value shall be updated
to the value specified in the current version of the INF spec.
3. The TianoCore wiki documents are written generically (and may not be
updated every time a specification is changed). As such, the wiki pages
may have incorrect versions of the ```INF_VERSION``` values.

**Rationale**

Tools that process the EDK II INF files may use this value to determine 
whether the tool can process all information in the file.

* Some tools may choose to provide warning messages, while other tools may 
give error messages.
* Some tools may choose to examine content that was defined at the time of the
spec release, and ignore content that was introduced in later versions of the 
specification.


## FILE_GUID value

This value shall be changed when a non-backward compatible change is made
to the INF file from a change to the module's code.

There are many tools available to create new GUID values. There is a Web
site where a GUID can be generated:  http://www.guidgen.com.  Microsoft
Visual Studio also has a GUID generator, uuidgen. Linux distributions may
also come with a GUID generator, such as uuid.

**Rationale**

Tools may use the ```FILE_GUID``` value (along with the 
```VERSION_STRING```) to determine whether non-backward compatible changes
have been made to the module. This value may also be used by design rule
checking tools.

For example, EDK II's UEFI Packaging Tool, UEFIPT, provided with the EDK II
BaseTools, uses this value during UDP creation. During installation, UEFIPT
uses this value (along with the VERSION_STRING value) to follow dependency
rules defined by the UDP spec.

Non-backward compatible changes may cause build errors, when a module no
longer produces a GUID, PROTOCOL or PPI that was produced in a previous
version of the module.

* Examples of **non-backward compatible changes** requiring a GUID change 
include, but are not limited to the following:
    * A GUID is no longer produced
    * A PROTOCOL is no longer produced
    * A PPI is no longer produced
    * Adding a DEC file in the [Packages] section
    * Changing a PROTOCOL, PPI or GUID's USAGE from ```CONSUMES``` to 
    ```PRODUCES```
    * A PCD's access method was changed in the code, such as using 
    ```PcdSetEx``` instead of ```PcdSet``` macros
    * A PCD's access method was changed due to an access method change
    in the DEC file that declared the PCD
    * A PCD from one package is replaced by a PCD from another EDK II package
    * Adding or changing entries to a DEPEX expression
 

* Examples of **backward compatible changes** not requiring a GUID change include,
but are not limited to the following:
    * Removing a Library Class dependency
    * Removing a DEC file in the [Packages] section
    * Changing a ```SOMETIMES_PRODUCES``` or ```SOMETIMES_CONSUMES``` to 
    ```PRODUCES``` or ```CONSUMES```
    * Removing entries from the DEPEX expression
    * Adding additional .C or .UNI files to a module (such as splitting a
    single .C file into .C and .H files)
    * Removing a GUID, PROTOCOL or PPI that had a ```USAGE``` of 
    ```CONSUMES``` or ```SOMETIMES_CONSUMES```
    * Adding a GUID, PROTOCOL or PPI

 
## VERSION_STRING value

The version number is used to track changes to an EDK II module, such as
adding a new function. The value should increment when new features are 
added, however, there are no hard and fast rules about updating the 
```VERSION_STRING``` value. 

**Rationale**

Tools may use this value to determine if new functionality has been added 
to the module.

New content and functionality implies a change to the Description of a Module 
Surface Area.

The value consists of a major number and an optional minor number. Best 
practices suggest using both a major and minor number.

## Best Practices

* When the ```FILE_GUID``` value changes:
    - Increment the major number and reset the minor number to 0.


* When the ```FILE_GUID``` value is unchanged: 
    - If new functionality is added due to new UEFI/PI Specification 
    releases, increment the 
    major number and reset the minor number to 0.
    - If new functionality is added due to other Industry Standard 
    Specification releases, increment the major number and reset the 
    minor number to 0.
    - If new functionality is added due to other specifications, 
    increment the major number and reset the minor number to 0.


* When the ```FILE_GUID``` and major number are not changed:
    - If new functionality is added (not a result of an update to any
    specification), increment the minor number. 
    - Increment the minor number only if new content is added (see below).
    - Increment the minor number only if content changes require an update
    (see below).


* Examples of **new functionality requiring an update** to the 
```VERSION_STRING``` include, but are not limited to the following:
    - Requiring a new library class for the module to function
    - Consuming or producing a new GUID
    - Consuming or producing a new PROTOCOL
    - Consuming or producing a new PPI
    - Get/Set a new PCD
    - Adding support for another module type


* Examples of **new content requiring an update** to the 
```VERSION_STRING``` include, but are not limited to the following:
    - Adding new key entries (```STR_```) to the ```MODULE_UNI_FILE```
    file
    - Adding comment block (defined by spec) content that maps to 
    attributes or entries defined in the UDP spec. such as, adding
    ```# USAGE``` or ```@PROMPT``` entries.
    - Adding an additional copyright (# Portions Copyright) line to
    the module INF.
    
 

* Examples of **content changes requiring an update** to the 
```VERSION_STRING``` include, but are not limited to the following:
    - Changing how the module is coded for PCD access methods
    from the general form to a restrictive form, such as PcdGetEx().
    - Stop producing a GUID, PROTOCOL or PPI.
    - Stop setting a PCD value
    - Changing the module's license
    - Adding tags (```STR_``` entries) in the ```MODULE_UNI_FILE```


* Examples of **content changes not requiring an update** to the
```VERSION_STRING``` include, but are not limited to the following:
    - Bug fixes in code
    - Spelling changes in comment content or text specified in
    entries in the ```MODULE_UNI_FILE```
    - Adding more help text in the INF or ```MODULE_UNI_FILE```
    - Adding new language translations of existing entries in the
    ```MODULE_UNI_FILE```
    - Changing the copyright date in INF or ```MODULE_UNIT_FILE```
    - Changing the Abstract or Description in the INF or 
    ```MODULE_UNI_FILE```

