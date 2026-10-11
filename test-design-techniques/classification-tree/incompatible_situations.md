[Back to Main Page](../../README.md)

[Back](./)

# Incompatible Situations (Environment Constraints) 

## The Concept
In combinatorial test design, **Incompatible Situations** occur when certain classes cannot logically or technically coexist. If a test generation tool (or a QA Engineer) blindly combines all inputs, it will generate "impossible" test cases. Attempting to execute these will result in blocked tests or false negatives. 

Identifying and documenting these constraints early saves significant test execution time.

## Scenario: Web Application Compatibility Matrix
We are testing a global enterprise web application. The application must be certified across various combinations of Operating Systems, Browsers, Localizations, and backend Databases.

### Requirements & Constraints:

| Identifier | Requirements                                                                                                                                                      | Traceability          | 
| :----:      | :---                                                                                                                                                             | :---                  |
| R01        | The application must be tested across supported OS, Browser, Localization, and Database configurations.                                                           | TC-V-01 - TC-V-04     |
| R02        | (Constraint) The **Safari** browser is strictly limited to the **Mac OS** environment.                                                                            | TC-InV-01             | 
| R03        | (Constraint) The **Internet Explorer** browser is strictly limited to the **Windows** environment.                                                                             | TC-InV-02             |
| R04        | (Constraint) **DB3** is a legacy database that lacks UTF-8 support; therefore, it is incompatible with **Arabic** and **Mandarin** localizations (English only).  | TC-InV-03             |


Based on these parameters, there is a [following Classification Tree](https://app.diagrams.net/#G1LGmr5C4NmzL2OUjF26MR92mzPRWVg0x3#%7B%22pageId%22%3A%22PDqzqBuKi--XkEUE9EO5%22%7D):

```mermaid
graph TD
    Root(["Config"])
    
    %% Classifications (Parameters)
    OS["OS"]
    Browser["Browser"]
    Localization["Localization"]
    Database["Database"]
    
    Root --> OS
    Root --> Browser
    Root --> Localization
    Root --> Database

    %% Define the style once
    classDef noBorder stroke-width:0px;

    %% Classes (Partitions) - Style applied directly using :::
    OS --> Linux["Linux"]:::noBorder
    OS --> Mac_OS["Mac OS"]:::noBorder
    OS --> Windows_1["Windows 1"]:::noBorder

    Browser --> Firefox["Firefox"]:::noBorder
    Browser --> Chromium["Chromium"]:::noBorder
    Browser --> Internet_Explorer["Internet Explorer "]:::noBorder
    Browser --> Safari["Safari"]:::noBorder
    Browser --> Chrome["Chrome"]:::noBorder

    Localization --> English["English"]:::noBorder
    Localization --> Arabic["Arabic"]:::noBorder
    Localization --> Mandarin["Mandarin"]:::noBorder

    Database --> DB1["DB1"]:::noBorder
    Database --> DB2["DB2"]:::noBorder
    Database --> DB3["DB3"]:::noBorder
```

## Combination Table (Handling Constraints)

When designing the test suite, we must actively filter out combinations that violate our constraints. Below is a sample of the test matrix showing both valid combinations and how invalid combinations are flagged.

> Note: TC-V - a valid test case,  TC-InV indicates an invalid test case that should be excluded from the test execution suite

| Test Case | OS | Browser | Localization | Database | Status / Traceability |
| :-- | :-- | :-- | :-- | :-- | :-- |
| TC-V-01 | Linux | Firefox | English | DB1 |  Valid (R01)|
| TC-V-02 | Mac OS | Safari | Mandarin | DB2 |  Valid (R01, R02) |
| TC-V-03 | Windows | Internet Explorer  | Arabic | DB1 |  Valid (R01, R03) |
| TC-V-04 | Windows | Firefox | English | DB3 |  Valid (R01, R04) |
| TC-InV-01 | Linux | Safari | English | DB2 |  Invalid (Violates R02) |
| TC-InV-02 | Mac OS | Internet Explorer  | Arabic | DB1 |  Invalid (Violates R03) |
| TC-InV-03 | Windows | Chrome | Mandarin | DB3 | Invalid (Violates R04) |



In a real-world scenario, feeding this tree into an automated combinatorial tool (like ACTS or PICT) without constraints would generate dozens of useless test cases (e.g., trying to boot Safari on Linux). By explicitly defining Incompatible Situations (R02-R04), we ensure the resulting test suite is 100% executable, highly efficient, and free of environmental false-positives. 

For full coverage, these classifications would be fed into a pairwise (2-wise) tool like PICT with the constraints (R02-R04) defined, generating a minimal set of valid, executable test cases. The table above shows representative valid and invalid combinations. 

---

See also:

* **[Classification Tree Examples](./README.md)** - More practical examples.
* **[Classification Tree Testing](https://olha-yatskivska.github.io/classification-tree.html)** -  Summary of the core concepts from ISTQB Advanced Test Analyst. 
* **[Classification Tree Tools](https://olha-yatskivska.github.io/classification-tree-tools.html)** - Links for the most popular tools.
* **[Back to Main Page](./)**
