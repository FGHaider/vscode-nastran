## [DTI,ESTDATA](https://help.hexagonmi.com/bundle/MSC_Nastran_2022.4/page/Nastran_Combined_Book/qrg/bulkde/TOC.DTI.ESTDATA.xhtml) - Superelement Estimation Data Overrides

Provides override data for time and space estimation for superelement processing operations.

#### Format:

```nastran
$---1---$---2---$---3---$---4---$---5---$---6---$---7---$---8---$---9---$---10--$
DTI     ESTDATA “0"                                                     +
+       kd1     vd1     kd2     vd2     -etc.-                          
```

The next entries are repeated for any superelement for which estimate data overrides are desired.  IREC must be incremented by 1.

```nastran
$---1---$---2---$---3---$---4---$---5---$---6---$---7---$---8---$---9---$---10--$
DTI     ESTDATA IREC    SEFLAG  SEID    k1      v1      k2      v2      +
+       k3      v3      -etc.-                                    
```

#### Example:

```nastran
$---1---$---2---$---3---$---4---$---5---$---6---$---7---$---8---$---9---$---10--$
DTI     ESTDATA  0                                                      +
+       NOMASS  -1                                                      
DTI     ESTDATA  1      SE      10      C1      5.5     C3      4.5     +
+       C7       7.3                                                    
```

```text
┌───────────┬───────────────────────────────────────────────────────────────────────────────────────────────────┐
│ Describer │ Meaning                                                                                           │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ kdi       │ Keyword for estimation parameter.  (Character from Table 0-1.)                                    │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ vdi       │ Value assigned to the estimation parameter kdi.  (The type given in Table 0-1.)                   │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ IREC      │ Record number beginning with 1.  (Integer > 0)                                                    │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ SEFLAG    │ SEFLAG = “SE” or “SEID” indicates the next field containing a superelement identification number. │
│           │  (Character)                                                                                      │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ SEID      │ Superelement identification number.  (Integer > 0)                                                │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ ki        │ Keyword for override of estimation parameter for indicated superelement.  (Character from         │
│           │ Table 0-1.)                                                                                       │
├───────────┼───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ vi        │ Value for keyword ki. (Type depends on ki as shown in the Table 0-1.)                             │
└───────────┴───────────────────────────────────────────────────────────────────────────────────────────────────┘
```

     See link for table.

#### Parameters Obtained from SEMAP

```text
┌─────┬─────────────────────────────────┐
│ NGI │ Number of interior grid points. │
├─────┼─────────────────────────────────┤
│ NPE │ Number of exterior grid points. │
├─────┼─────────────────────────────────┤
│ NS  │ Number of scalar points         │
├─────┼─────────────────────────────────┤
│ NE  │ Number of elements.             │
└─────┴─────────────────────────────────┘
```

#### Derived Parameters

```text
┌────────────────┐
│ Size of o-set. │
├────────────────┤
│ Size of a-set. │
├────────────────┤
│ Number of      │
│ matrix terms   │
│ in a buffer.   │
└────────────────┘
```

#### Estimation Equations

For each superelement, estimates of CPU time and disk space are made using the following equations.

     See link for table.

#### Remarks:

1. In the superelement solution sequences, this data is stored automatically.
2. The header record continuation entries are optional if no global override data is to be specified. In this case, the complete header entry is optional.
     - Active column data can come from one of several places. The value for CRMS is determined as follows:
     - RMS from the entry when IREC > 0 and field 4 is “SE”.
     - RMS from entries with IREC = 0.
     - Computed bandwidth when PARAM,OLDSEQ is specified.
     - If FCRMS is specified when IREC > 0 and field 4 is “SE”, then CRMS =  ![bulkde03332.jpg](https://help-be.hexagonmi.com/bundle/MSC_Nastran_2022.4/page/Nastran_Combined_Book/qrg/bulkde/../../../assets/bulkde03332.jpg?_LANG=enus) .
     - If FCRMS is specified when IREC = 0, then CRMS =  ![bulkde03334.jpg](https://help-be.hexagonmi.com/bundle/MSC_Nastran_2022.4/page/Nastran_Combined_Book/qrg/bulkde/../../../assets/bulkde03334.jpg?_LANG=enus) .
     - CRMS =  ![bulkde03336.jpg](https://help-be.hexagonmi.com/bundle/MSC_Nastran_2022.4/page/Nastran_Combined_Book/qrg/bulkde/../../../assets/bulkde03336.jpg?_LANG=enus) .
3. If CMAX is not specified, then it is defaulted to CRMS.
4. In the example above, mass terms are excluded for all superelements and new values are given for parameters C1, C3, and C7 for Superelement 10 only.
5. The estimates for TSEX, SSEX, and TWALLX are not printed unless at least one estimate exceeds the threshold.
