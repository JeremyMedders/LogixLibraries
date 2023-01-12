# LogixLibraries

Collections of UDIs, UDTs, and sample programs written in Studio 5000 v35.

This is my concentrated best-effort approach to implementing object-oriented programming on Rockwell Logix5000-based controllers.

Parameter naming follows PlantPAx standards, where sensible:
- Inp_
- Out_
- Sts_
- Val_
- Cfg_
- Wrk_: Avoided using this for local AOI tags (forgoing a prefix distinguishes them from AOI parameters). 

Blocks (AO_) are organized into groups:
- Dvc: Device drivers
- Math: Assorted function blocks
- MBTCP: Modbus TCP client driver
- Op: Light-weight PlantPAx-style blocks 
- Msg: Message utilities
- RTC: Precision pulse/timing utilites
- Str: String utilities
- Sys: System diagnostic classes and utilities

Source edit protection is enabled, but the code is viewable (it may make sense to fully unlock it but I'm also learning Git, so bear with me).

With the exception of complementary FactoryTalk View files, this repository contains only .L5X (Logix XML) files.

The structured text language is generally used for add-on-instruction definitions for ease of portability between IEC 61131-3 platforms.

Type and instruction dependencies will be documented where possible.

Some add-on-instructions make use of unsigned (USINT/UINT/UDINT/ULINT) and 64-bit (ULINT/LINT) types, limiting their use to current-generation hardware (CompactLogix 5380, CompactLogix 5480, and ControlLogix 5580 families) and future releases. CompactLogix 5370, ControlLogix 5570 and earlier families are unfortunately artificially limited to signed types (SINT/INT/DINT/LINT), so instructions will need to be modified to accomodate where necessary.
