# LogixLibraries

This is my best-effort approach to implementing production-ready, "object-oriented" and "functional" styles of programming on Rockwell Logix5000 controllers.

With the exception of supporting sample files (FactoryTalk View ME screens/definitions, etc.), this repository contains only .L5X (Logix 5000 XML) files. Structured text is used for AOI definitions to ease porting between IEC 61131-3 platforms. Dependencies will be documented where possible.

Parameter naming follows PlantPAx (sensibly)
------------
- Inp_
- PCmd_, OCmd_, MCmd, XCmd
- PSet_, OSet_, MSet, XSet
- Out_
- Sts_
- Val_
- Cfg_
- Wrk_: Avoided using this for local AOI tags (forgoing a prefix distinguishes them from AOI parameters).
- Rdy_: Avoided in favor of consolidating under the Sts_ prefix.
- At times, parameter names were modified for consistency / clarity, particularly with my CmdSrc substitute.
- External access (Read, Read/Write, None) are set where sensible.

AOIs/UDTs (AO_/ST_) built as classes
------------
- Dvc: Device drivers. Each of these embed an AO_Sys_Dvc that automagically handles registration and reporting to its parent AO_Sys_DvcClass.
- Math: Assorted function blocks.
- MBTCP: Modbus TCP client driver.
- Op: Lightweight PAx-style blocks. Parameter naming and layout isn't necessarily 1:1 with their PAx counterpart. 
- Msg: Message helpers and utilities.
- RTC: Precision pulse/timing utilites.
- Str: String utilities.
- Sys: System diagnostics, WallClock utility/formatting generator, ISA 18.2 alarming with its parent "class", and other utilities.
- UI: HMI helper blocks. Includes List Selector object with support for variable rows and unlimited columns of data.

UDTs follow the corresponding AOI in name:
- ST_Dvc_abc
- ST_Sys_xyz
- And so on.
- External access (Read, Read/Write, None) are set where sensible.

AOI variants (future)
------------
Depending on use case, some of the features of an AOI will go unused. Tentatively, I think a simple suffix to the block name could differentiate it from others. Example:
- AO_Dvc_PF525: Full features. Drive parameters managed and updated dynamically from the PLC using added Class 3 messaging.
- AO_Dvc_PF525_L: Light version. Block capable of running the device but limited to the scope of its Class 1 connection data. Unused block parameters deleted.
- Both of these would still contain an "Op" strategy Command Source block and identitical core Local data to keep overall UDT sprawl to a minimum.

So we have...
- No suffix: base/full
- L: Light
- M/T: Mirror/Monitor or Twin. This would be an AOI in structure only, no other code. Perhaps useful for a monitoring or concentrator PLC/DCS.
- S: Simulator

Extras
------------
- UDT templates to aid in implementing the useful BIT overlay construct.
- IO module / connection templates.

To-Do
------------
- performance profiling database
- documentation about known working .L5X attribute values
- how to put the CanBeNull parameter attribute in AOIs to use
- documentation for the Alarm family
- design pattern guides and rationale
- overall repository structure improvements
- MBTCP client basic documentation
- documentation for the PowerFlex 525
- OSCAT library port
- Arduino PLC data exchange
- pointers vs. InOut / ByRef data handling and (safe!) examples
- AOI dependency chart/tree/spreadsheet
- Produce/Consume tags "the smart way" guide with UDTs and sample
- PackML starter guide and sample

Done:
- open discussion board

"Legacy" hazards
------------
- Some of the library content makes use of unsigned (USINT/UINT/UDINT/ULINT) and 64-bit (ULINT/LINT) types, limiting their use to current-generation hardware (CompactLogix 5380/5480 and ControlLogix 5580 families).
- Logix 5370/5570 and earlier families are unfortunately artificially limited to signed types (SINT/INT/DINT/LINT), so code will need to be modified to accomodate where necessary. I built this library to be as lean as possible, so the backwards accomodation would have ended up bloating solutions across the division.
- Sample code heavily favors program-scoped tags to promote organization and consistent naming. For that reason, these sample programs will sometimes have program-scoped Messages and will require accomodation for pre-5x80 hardware.

Always
------------
- Engineer to win.
- Feel free to ask any questions.
- Please provide any feedback you have.

JeremyM
