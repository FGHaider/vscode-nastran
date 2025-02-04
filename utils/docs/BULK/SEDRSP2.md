## [SEDRSP2](https://help.hexagonmi.com/bundle/MSC_Nastran_2022.4/page/Nastran_Combined_Book/qrg/bulkqrs/TOC.SEDRSP2.xhtml) - Design Sensitivity Equation Response Quantities for PART SE

Defines equation responses that are used in the design, either as constraints or as an objective with quantities from multiple PART SEs.

#### Format:

```nastran
$---1---$---2---$---3---$---4---$---5---$---6---$---7---$---8---$---9---$---10--$
SEDRSP2 ID      LABEL   EQID ...REGION  METHOD  C1      C2      C3      +       
+       “DESVAR”DVSEID1 DVID1   DVSEID2 DVID2   DVSEID3 DVID3           +       
+               DVSEID4 DVID4   -etc.-                                  +       
+       “DTABLE”LBSEID1 LABL1   LBSEID2 LABL2   LBSEID3 LABL3           +       
+               LBSEID4 LABL4   -etc.-                                  +       
+       “DRESP1”R1SEID1 NR1     R1SEID2 NR2     R1SEID3 NR3             +       
+               R1SEID4 NR4     -etc.-                                  +       
+       “DNODE” NDSEID1 G1      CMP1    NDSEID2 G2      CMP2            +       
+               NDSEID3 G3      CMP3    -etc.-                          +       
+       “DVPREL1P1SEID1 DPIP1   P1SEID2 DPIP2   P1SEID3 DPIP3           +       
+               P1SEID4 DPIP4   -etc.-                                  +       
+       “DVCR...C1SEID1 DCIC1   C1SEID2 DCIC2   C1SEID3 DCIC3           +       
+               C1SEID4 DCIC4   -etc.-                                  +       
+       “DVMR...M1SEID1 DMIM1   M1SEID2 DMIM2   M1SEID3 DMIM3           +       
+               M1SEID4 DMIM4   -etc.-                                  +       
+       “DVPR...P2SEID1 PDI2P1  P2SEID2 DPI2P2  P2SEID3 DPI2P3          +       
+               P2SEID4 DPI2P4  -etc.-                                  +       
+       “DVCR...C2SEID1 DC12C1  C2SEID2 DC12C2  C2SEID3 DC12C3          +       
+               C2SEID4 DCI2C4  -etc.-                                  +       
+       “DVMR...M2SEID1 DM12M1  M2SEID2 DMI2M2  M2SEID3 DM12M3          +       
+               M2SEID4 DMI2M4  -etc.-                                          
```

#### Example:

```nastran
$---1---$---2---$---3---$---4---$---5---$---6---$---7---$---8---$---9---$---10--$
SEDRSP2 1       LBUCK   5       3                                       +       
+       DESVAR  0       101     1       3       1       4               +       
+               10      201                                             +       
+       DTABLE  1       YM      10      L                               +       
+       DRESP1  0       14      1       1       1       4               +       
+       DNODE   10      14      0       1                               +       
+       DVPREL1 0       101     1       102                             +       
+       DVCREL1 1       201     10      202                             +       
+       DVMREL1 0       301                                             +       
+       DVPREL2 10      401     1       402                             +       
+       DVCREL2 0       501                                             +       
+       DVMREL2 0       601     1       602     10      603                     
```

```text
┌───────────┬───────────────────────────────────────────────────────────────────────────────────────────────────┐
│ Describer │ Meaning                                                                                           │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ ID        │ Unique identification number. (Integer > 0)                                                       │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ LABEL     │ User-defined label. (Character)                                                                   │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ EQID      │ DEQATN entry identification number. (Integer > 0)                                                 │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ FUNC      │ Function to be applied to the arguments. See Remark 8. of the DRESP2 entry. (Character)           │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ REGION    │ Region identifier for constraint screening. See Remark 5. of the DRESP2 entry. (Integer > 0)      │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ METHOD    │ When used with FUNC = BETA, METHOD = MIN indicates a minimization task while MAX indicates a      │
│           │ maximization task. (Default = MIN) When used with FUNCT = MATCH, METHOD = LS indicated a least    │
│           │ squares while METHOD = BETA indicated minimization of the maximum difference. (Default = LS)      │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Ci        │ Constants used when FUNC = BETA or FUNC = MATCH in combination with METHOD = BETA. See Remark     │
│           │ 8. of the DRESP2 entry. (Real; Defaults: C1 = 100., C2 = .005)                                    │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ “DESVAR”  │ Flag indicating DESVAR entry identification numbers. (Character)                                  │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ DVSEIDi   │ PART SE identification number for DVIDi (Integer > 0)                                             │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ DVIDi     │ DESVAR entry identification number. (Integer > 0)                                                 │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ “DTABLE”  │ DTABLE flag. Indicates that the LABLs for the constants in a DTABLE or DTABLE2 entry follow. This │
│           │ field may be omitted if there are no constants involved in this relation. (Character)             │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ LBSEIDj   │ PART SE identification number for LABLj. (Integer > 0)                                            │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ LABLi     │ Label for a constant on the DTABLE or DTABLE2 entry. (Character)                                  │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ “DRESP1”  │ Flag indicating DRESP1 entry identification numbers. (Character)                                  │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ R1SEIDk   │ PART SE identification number for NRk. (Integer > 0)                                              │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ NRk       │ DRESP1 entry identification number. (Integer > 0)                                                 │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ “DNODE”   │ Flag indicating grid point and component identification numbers. (Character)                      │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ NDSEIDm   │ PART SE identification number for (Gm,Cm). (Integer > 0)                                          │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Gm        │ Identification number for any grid point in the model. (Integer > 0)                              │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Cm        │ Component number of grid point Gm. (1 < Integer < 3)                                              │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ “DVPREL1” │ Flag indicating DVPREL1 entry identification number. (Character)                                  │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ P1SEIDi   │ PART SE identification number for DPIPi. (Integer > 0)                                            │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ DPIPi     │ DVPREL1 entry identification number. (Integer > 0)                                                │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ “DVCREL1” │ Flag indicating DVCREL1 entry identification number. (Character)                                  │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ C1SEIDi   │ PART SE identification number for DCICi. (Integer > 0)                                            │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ DCICi     │ DVCREL1 entry identification number. (Integer > 0)                                                │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ “DVMREL1” │ Flag indicating DVPREL2 entry identification number. (Character)                                  │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ M1SEIDi   │ PART SE identification number for DMIMi. (Integer > 0)                                            │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ DMIMi     │ DVMREL1 entry identification number. (Integer > 0)                                                │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ “DVPREL2” │ Flag indicating DVPREL2 entry identification number. (Character)                                  │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ P2SEIDi   │ PART SE identification number for DPI2Pi. (Integer > 0)                                           │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ DPI2Pi    │ DVPREL2 entry identification number. (Integer > 0)                                                │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ “DVCREL2” │ Flag indicating DVCREL2 entry identification number. (Character)                                  │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ C2SEIDi   │ PART SE identification number for DCI2Ci. (Integer > 0)                                           │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ DCI2Ci    │ DVCREL2 entry identification number. (Integer > 0)                                                │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ “DVMREL2” │ Flag indicating DVMREL2 entry identification number. (Character)                                  │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ M2SEIDi   │ PART SE identification number for DMI2Mi. (Integer > 0)                                           │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ DMI2Mi    │ DVMREL2 entry identification number. (Integer > 0)                                                │
└───────────┴───────────────────────────────────────────────────────────────────────────────────────────────────┘
```
