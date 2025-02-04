## [EQUILIBRIUM (Case)](https://help.hexagonmi.com/bundle/MSC_Nastran_2022.4/page/Nastran_Combined_Book/qrg/casecontrol4a/TOC.EQUILIBRIUM.Case.xhtml) - Equilibrium Force Output Request

Specifies options for equilibrium force balance output of applied loads, single point constraint forces and forces due to multi-point constraints and rigid elements.

#### Format:

![casecontrol4a00918.jpg](https://help-be.hexagonmi.com/bundle/MSC_Nastran_2022.4/page/Nastran_Combined_Book/qrg/casecontrol4a/../../../assets/casecontrol4a00918.jpg?_LANG=enus)  

#### Examples:

```nastran
EQUILIBRIUM
EQUILIBRIUM = 501
```

```text
┌──────────────┬────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ Describer    │ Meaning                                                                                            │
├──────────────┼────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ PRINT or     │                                                                                                    │
│ (blank)      │                                                                                                    │
├──────────────┼────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ PUNCH        │                                                                                                    │
├──────────────┼────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ PLOT         │                                                                                                    │
├──────────────┼────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ * The .op2 binary database file will be generated with “PARAM,POST, X” (or the POST Case Control command), while  │
│ the .h5 binary database file will be generated with “HDF5OUT” entry specified in Bulk Data Section.  Both .op2    │
│ and .h5 file can be created simultaneously. Note .xdb file is being deprecated.                                   │
├──────────────┼────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ YES          │ Requests moment summation referenced to origin of basic coordinate system.                         │
├──────────────┼────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ gid          │ Requests moment summation referenced to basic system location specified by the coordinates of grid │
│              │ point gid.                                                                                         │
├──────────────┼────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ NONE         │ Equilibrium force balance output will not be generated.                                            │
└──────────────┴────────────────────────────────────────────────────────────────────────────────────────────────────┘
```

#### Remarks:

1. The EQUILIBRIUM Case Control command produces a summary of the applied loads, single point forces of constraint (SPC), and multipoint/rigid body element forces of constraint (MPC), as well as a summation of these quantities. In order for the summation to represent all of the forces in the problem, these forces must be available and, therefore, the specification of an EQUILIBRIUM Case Control command causes the program to automatically compute the SPC and MPC forces. However, if desired, the associated Case Control commands should request output. The single point forces of constraint are requested by the presence of an SPCFORCE command, and the multipoint/RBE constraint forces are requested by an MPCFORCE command. Applied loads are automatically generated by the presence of the LOAD selection Case Control command.
2. Results are always output in the basic coordinate system.
3. The EQUILIBRIUM Case Control command is applicable to Linear Static analysis (SOL101) only, and does not produce output if any superelements are present.
