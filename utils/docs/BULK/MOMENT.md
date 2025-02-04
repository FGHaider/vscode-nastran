## [MOMENT](https://help.hexagonmi.com/bundle/MSC_Nastran_2022.4/page/Nastran_Combined_Book/qrg/bulkno/TOC.MOMENT.xhtml) - Static Moment

Defines a static concentrated moment at a grid point by specifying a scale factor and a vector that determines the direction.

#### Format:

```nastran
$---1---$---2---$---3---$---4---$---5---$---6---$---7---$---8---$---9---$---10--$
MOMENT  SID     G       CID     M       N1      N2      N3                      
```

#### Example:

```nastran
$---1---$---2---$---3---$---4---$---5---$---6---$---7---$---8---$---9---$---10--$
MOMENT  2       5       6       2.9     0.0     1.0     0.0                     
```

```text
┌───────────┬─────────────────────────────────────────────────────────────────────────────────────────────────┐
│ Describer │ Meaning                                                                                         │
├───────────┼─────────────────────────────────────────────────────────────────────────────────────────────────┤
│ SID       │ Load set identification number.  (Integer > 0)                                                  │
├───────────┼─────────────────────────────────────────────────────────────────────────────────────────────────┤
│ G         │ Grid point identification number at which the moment is applied.  (Integer > 0)                 │
├───────────┼─────────────────────────────────────────────────────────────────────────────────────────────────┤
│ CID       │ Coordinate system identification number.  (Integer > 0 or blank)                                │
├───────────┼─────────────────────────────────────────────────────────────────────────────────────────────────┤
│ M         │ Scale factor.  (Real)                                                                           │
├───────────┼─────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Ni        │ Components of the vector measured in the coordinate system defined by CID.  (Real; at least one │
│           │ Ni0.0 unless M is zero)                                                                         │
└───────────┴─────────────────────────────────────────────────────────────────────────────────────────────────┘
```

#### Remarks:

1. The static moment applied to grid point G is given by

     ![bulkno06010.jpg](https://help-be.hexagonmi.com/bundle/MSC_Nastran_2022.4/page/Nastran_Combined_Book/qrg/bulkno/../../../assets/bulkno06010.jpg?_LANG=enus)  

     where  ![bulkno06012.jpg](https://help-be.hexagonmi.com/bundle/MSC_Nastran_2022.4/page/Nastran_Combined_Book/qrg/bulkno/../../../assets/bulkno06012.jpg?_LANG=enus)  is   the vector defined by (N1, N2, N3).  The magnitude of  ![bulkno06014.jpg](https://help-be.hexagonmi.com/bundle/MSC_Nastran_2022.4/page/Nastran_Combined_Book/qrg/bulkno/../../../assets/bulkno06014.jpg?_LANG=enus)  is equal to M times the magnitude of  ![bulkno06016.jpg](https://help-be.hexagonmi.com/bundle/MSC_Nastran_2022.4/page/Nastran_Combined_Book/qrg/bulkno/../../../assets/bulkno06016.jpg?_LANG=enus) .

2. In the static solution sequences, SID must be selected by the LOAD Case Control command.

     In the dynamic solution sequences, if there is a LOADSET Case Control command, then SID must be referenced in the LID field of a selected LSEQ entry.  If there is no LOADSET Case Control command, then SID must be referenced in the EXCITEID field of an RLOADi or TLOADi entry.

3. A CID of zero or blank references the basic coordinate system.
4. For scalar points see SLOAD.
5. For TYPE=12 or TYPE=13 on the TLOAD1, G is the ID of a rigid body: the MID of a rigid material (MATRIG) or the EID of a RBE2D. The MID of a rigid material and the EID of RBE2 must be different when both of a RBE2D and a rigid material are used with these TYPEs. SOL 700 only.
