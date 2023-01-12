# LogixLibraries

Collections of UDIs, UDTs, and sample programs written in Studio 5000 v35.

This is my concentrated best-effort approach to implementing object-oriented programming on Rockwell Logix5000-based controllers. Source edit protection is enabled, but the code is viewable (it may make sense to fully unlock it but I'm also learning Git, so bear with me).

With the exception of complementary sample files (FactoryTalk View, and so on), this repository contains only .L5X (Logix 5000 XML) files. Structured text is used for add-on-instruction definitions for ease of portability between IEC 61131-3 platforms. Type and instruction dependencies will be documented where possible.

Parameter naming follows PlantPAx standards, where sensible:
- Inp_
- PCmd_, OCmd_, MCmd, XCmd
- PSet_, OSet_, MSet, XSet
- Out_
- Sts_
- Val_
- Cfg_
- Wrk_: Avoided using this for local AOI tags (forgoing a prefix distinguishes them from AOI parameters).
- Rdy_: Avoided in favor of consolidating under the Sts_ prefix.
- External access (Read, Read/Write, None) are set where sensible.

AOIs (AO_) are organized into groups:
- Dvc: Device drivers
- Math: Assorted function blocks
- MBTCP: Modbus TCP client driver.
- Op: Light-weight PlantPAx-style blocks. Parameter naming and layout isn't necessarily 1:1 with their PlantPAx counterpart. 
- Msg: Message utilities
- RTC: Precision pulse/timing utilites
- Str: String utilities
- Sys: System diagnostic "classes", ISA 18.2 alarming and its "class",  and utilities

UDTs (ST_) follow the AOI grouping in name:
- ST_Dvc_
- ST_Sys_
- And so on.
- External access (Read, Read/Write, None) are set where sensible.

Will also be including:
- some UDT templates to aid others in implementing the useful BIT overlay construct.
- some explanatory documentation about known working L5X attribute values.
- a demonstration of using the CanBeNull parameter attribute in AOIs.

Some add-on-instructions make use of unsigned (USINT/UINT/UDINT/ULINT) and 64-bit (ULINT/LINT) types, limiting their use to current-generation hardware (CompactLogix 5380, CompactLogix 5480, and ControlLogix 5580 families) and future releases. CompactLogix 5370, ControlLogix 5570 and earlier families are unfortunately artificially limited to signed types (SINT/INT/DINT/LINT), so code will need to be modified to accomodate where necessary. I built this library to be as lean as possible, so the backwards accomodation would have ended up bloating solutions across the division.
