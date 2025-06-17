# Semantic Versioning 3.0.0_0 - Mermaid Diagrams

To enhance the understanding of the **Semantic Versioning 3.0.0_0** framework, the following Mermaid diagrams have been created. These diagrams visually represent the versioning structure, incrementing rules, precedence comparison, and the overall versioning workflow.

---

## 1. Version Number Structure

This diagram illustrates the components of the Semantic Versioning 3.0.0_0 version number format.

```mermaid
graph LR
    A[MAJOR] --> B[MINOR]
    B --> C[PATCH]
    C --> D[RELEASE]
    D --> E[METADATA]
    
    subgraph Version_Number_Structure
        MAJOR[MAJOR: Incompatible API Changes]
        MINOR[MINOR: Backward-Compatible Functionality]
        PATCH[PATCH: Backward-Compatible Bug Fixes]
        RELEASE[RELEASE: Pre-Release Identifiers]
        METADATA[METADATA: Build Information]
    end
    
    MAJOR --> MINOR
    MINOR --> PATCH
    PATCH --> RELEASE
    RELEASE --> METADATA

```

### Explanation:
- **MAJOR:** Indicates incompatible API changes.
- **MINOR:** Denotes the addition of functionality in a backward-compatible manner.
- **PATCH:** Represents backward-compatible bug fixes.
- **RELEASE:** Signifies pre-release identifiers (e.g., alpha, beta, rc).
- **METADATA:** Contains build metadata for additional context.

---

## 2. Incrementing Rules Flowchart

This flowchart guides the decision-making process for incrementing different components of the version number based on the type of changes made.

```mermaid
flowchart TD
    Start[Start] --> Action{Type of Change}
    
    Action -->|Incompatible API Changes| IncrementMajor
    Action -->|Add Backward-Compatible Functionality| IncrementMinor
    Action -->|Backward-Compatible Bug Fixes| IncrementPatch
    Action -->|Pre-Release Iteration| IncrementRelease
    Action -->|Append Build Metadata| AppendMetadata
    
    IncrementMajor["Increment MAJOR<br/>Reset MINOR, PATCH, RELEASE to 0"]
    IncrementMinor["Increment MINOR<br/>Reset PATCH and RELEASE to 0"]
    IncrementPatch["Increment PATCH<br/>Reset RELEASE to 0"]
    IncrementRelease["Increment RELEASE Identifier"]
    AppendMetadata["Append Build Metadata<br/>(e.g., +build.123)"]
    
    IncrementMajor --> End[End]
    IncrementMinor --> End
    IncrementPatch --> End
    IncrementRelease --> End
    AppendMetadata --> End
```

### Explanation:
- **Incompatible API Changes:** Increment the MAJOR version and reset MINOR, PATCH, and RELEASE to `0`.
- **Add Backward-Compatible Functionality:** Increment the MINOR version and reset PATCH and RELEASE to `0`.
- **Backward-Compatible Bug Fixes:** Increment the PATCH version and reset RELEASE to `0`.
- **Pre-Release Iteration:** Increment the RELEASE identifier for new pre-release versions.
- **Append Build Metadata:** Append build metadata using the `+` delimiter.

---

## 3. Version Precedence Comparison

This diagram demonstrates how different version numbers are compared to determine their precedence.

```mermaid
graph TD
    A[Compare MAJOR] --> B{Equal?}
    B -->|No| C[Higher MAJOR Wins]
    B -->|Yes| D[Compare MINOR]
    D --> E{Equal?}
    E -->|No| F[Higher MINOR Wins]
    E -->|Yes| G[Compare PATCH]
    G --> H{Equal?}
    H -->|No| I[Higher PATCH Wins]
    H -->|Yes| J[Compare RELEASE]
    J --> K{Presence of RELEASE}
    K -->|No| L[Higher Precedence]
    K -->|Yes| M[Compare RELEASE Identifiers]
    M --> N{Higher RELEASE Wins}
    
    style A fill:#f9f,stroke:#333,stroke-width:2px
    style B fill:#bbf,stroke:#333,stroke-width:2px
    style C fill:#bfb,stroke:#333,stroke-width:2px
    style D fill:#bbf,stroke:#333,stroke-width:2px
    style E fill:#bbf,stroke:#333,stroke-width:2px
    style F fill:#bfb,stroke:#333,stroke-width:2px
    style G fill:#bbf,stroke:#333,stroke-width:2px
    style H fill:#bbf,stroke:#333,stroke-width:2px
    style I fill:#bfb,stroke:#333,stroke-width:2px
    style J fill:#bbf,stroke:#333,stroke-width:2px
    style K fill:#bbf,stroke:#333,stroke-width:2px
    style L fill:#bfb,stroke:#333,stroke-width:2px
    style M fill:#bbf,stroke:#333,stroke-width:2px
    style N fill:#bfb,stroke:#333,stroke-width:2px
```

### Explanation:
1. **Compare MAJOR:** Versions with higher MAJOR numbers have higher precedence.
2. **Compare MINOR:** If MAJOR versions are equal, compare MINOR versions.
3. **Compare PATCH:** If both MAJOR and MINOR are equal, compare PATCH versions.
4. **Compare RELEASE:** If MAJOR, MINOR, and PATCH are equal, versions without a RELEASE identifier have higher precedence than those with one. If both have RELEASE identifiers, compare them lexically and numerically.

**Examples:**
- `1.0.0_0` < `1.0.0_1`
- `1.0.0_1` < `1.0.0_2`
- `1.0.0_2` < `1.0.1_0`
- `1.1.0_0` < `2.0.0_0`

---

## 4. Versioning Workflow

This diagram outlines the typical workflow of versioning from initial development to maintenance using Semantic Versioning 3.0.0_0.

```mermaid
graph TD
    Start[Initial Development] --> Prototype[Prototype Phase]
    Prototype --> Alpha[Alpha Pre-Release]
    Alpha --> BugFix1[Bug Fix in Prototype]
    BugFix1 --> MVP[MVP Launch]
    MVP --> NewFeature[Add New Feature to MVP]
    NewFeature --> InternalAlpha[Internal Alpha Release]
    InternalAlpha --> ExternalBeta[External Beta Release]
    ExternalBeta --> BugFix2[Bug Fix in Beta]
    BugFix2 --> Production[Final Production Deployment]
    Production --> MajorRelease[Major Release with Incompatible Changes]
    MajorRelease --> MaintenanceFeature[Maintenance Feature Addition]
    MaintenanceFeature --> MaintenanceBugFix[Maintenance Bug Fix]
    MaintenanceBugFix --> MaintenanceMetadata[Maintenance Release with Metadata]
    MaintenanceMetadata --> End[End]
    
    classDef phase fill:#f9f,stroke:#333,stroke-width:2px;
    classDef action fill:#bbf,stroke:#333,stroke-width:2px;
    
    class Start,End phase;
    class Prototype,Alpha,BugFix1,MVP,NewFeature,InternalAlpha,ExternalBeta,BugFix2,Production,MajorRelease,MaintenanceFeature,MaintenanceBugFix,MaintenanceMetadata action;
```

### Explanation:
1. **Initial Development:** Start with version `0.0.0_0`.
2. **Prototype Phase:** Increment MINOR for initial feature additions (e.g., `0.1.0_0`).
3. **Alpha Pre-Release:** Release an alpha version (e.g., `0.1.0_1`).
4. **Bug Fix in Prototype:** Increment PATCH for bug fixes (e.g., `0.1.1_0`).
5. **MVP Launch:** Transition to MVP with MAJOR version increment (e.g., `1.0.0_0`).
6. **Add New Feature to MVP:** Increment MINOR for new features (e.g., `1.1.0_0`).
7. **Internal Alpha Release:** Release an internal alpha version (e.g., `1.1.0_1`).
8. **External Beta Release:** Release an external beta version (e.g., `1.1.0_2`).
9. **Bug Fix in Beta:** Increment PATCH for bug fixes (e.g., `1.1.1_0`).
10. **Final Production Deployment:** Deploy to production with metadata (e.g., `1.1.1_1+build.123`).
11. **Major Release with Incompatible Changes:** Increment MAJOR and append new metadata (e.g., `2.0.0_0+build.456`).
12. **Maintenance Feature Addition:** Increment MINOR during maintenance (e.g., `2.1.0_0+build.456`).
13. **Maintenance Bug Fix:** Increment PATCH during maintenance (e.g., `2.1.1_0+build.456`).
14. **Maintenance Release with Metadata:** Append metadata during maintenance (e.g., `2.1.1_1+build.789`).
15. **End:** Lifecycle concludes.

---

## 5. BNF Grammar Representation

While Mermaid does not natively support BNF grammar diagrams, the adapted Backus–Naur Form (BNF) grammar can be represented using a flowchart to visualize the structure of valid Semantic Versioning 3.0.0_0 strings.

```mermaid
graph TD
    A["valid semver"] --> B["version core"]
    A --> C["version core (underscore) pre-release"]
    A --> D["version core (plus) build"]
    A --> E["version core (underscore) pre-release (plus) build"]
    
    B["version core"] --> F["major.minor.patch"]
    
    F --> G["major"]
    F --> H["minor"]
    F --> I["patch"]
    
    C --> J["pre-release"]
    D --> K["build"]
    E --> J
    E --> K
    
    J["pre-release"] --> L["dot-separated pre-release identifiers"]
    K["build"] --> M["dot-separated build identifiers"]
    
    L["dot-separated pre-release identifiers"] --> N["pre-release identifier"]
    L --> O["pre-release identifier.dot-separated pre-release identifiers"]
    
    M["dot-separated build identifiers"] --> P["build identifier"]
    M --> Q["build identifier.dot-separated build identifiers"]
    
    N["pre-release identifier"] --> R["alphanumeric identifier"]
    N --> S["numeric identifier"]
    
    P["build identifier"] --> T["alphanumeric identifier"]
    P --> U["digits"]
    
    %% Style for clarity
    classDef terminal fill:#f96,stroke:#333,stroke-width:1px;
    class G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U terminal;
```

### Explanation:
- **Valid SemVer:** The root node representing a valid semantic version.
- **Version Core:** Consists of MAJOR, MINOR, and PATCH.
- **Pre-Release and Build:** Optional components that can be appended to the version core.
- **Identifiers:** Define the structure of pre-release and build metadata.

---

## 6. Adapted Backus–Naur Form (BNF) Grammar

For a detailed representation of the adapted BNF grammar, refer to the **Adapted Backus–Naur Form (BNF) Grammar** section in the documentation.

```plaintext
<valid semver> ::= <version core>
                 | <version core> "_" <pre-release>
                 | <version core> "+" <build>
                 | <version core> "_" <pre-release> "+" <build>

<version core> ::= <major> "." <minor> "." <patch>

<major> ::= <numeric identifier>

<minor> ::= <numeric identifier>

<patch> ::= <numeric identifier>

<pre-release> ::= <dot-separated pre-release identifiers>

<dot-separated pre-release identifiers> ::= <pre-release identifier>
                                          | <pre-release identifier> "." <dot-separated pre-release identifiers>

<build> ::= <dot-separated build identifiers>

<dot-separated build identifiers> ::= <build identifier>
                                    | <build identifier> "." <dot-separated build identifiers>

<pre-release identifier> ::= <alphanumeric identifier>
                           | <numeric identifier>

<build identifier> ::= <alphanumeric identifier>
                     | <digits>

<alphanumeric identifier> ::= <non-digit>
                            | <non-digit> <identifier characters>
                            | <identifier characters> <non-digit>
                            | <identifier characters> <non-digit> <identifier characters>

<numeric identifier> ::= "0"
                       | <positive digit>
                       | <positive digit> <digits>

<identifier characters> ::= <identifier character>
                          | <identifier character> <identifier characters>

<identifier character> ::= <digit>
                         | <non-digit>

<non-digit> ::= <letter>
              | "-"

<digits> ::= <digit>
           | <digit> <digits>

<digit> ::= "0"
          | <positive digit>

<positive digit> ::= "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"

<letter> ::= "A" | "B" | "C" | "D" | "E" | "F" | "G" | "H" | "I" | "J"
           | "K" | "L" | "M" | "N" | "O" | "P" | "Q" | "R" | "S" | "T"
           | "U" | "V" | "W" | "X" | "Y" | "Z"
           | "a" | "b" | "c" | "d" | "e" | "f" | "g" | "h" | "i" | "j"
           | "k" | "l" | "m" | "n" | "o" | "p" | "q" | "r" | "s" | "t"
           | "u" | "v" | "w" | "x" | "y" | "z"
```

---

## 7. Conclusion

The **Semantic Versioning 3.0.0_0 - Mermaid Diagrams** documentation provides a comprehensive visual and descriptive guide to understanding and implementing the adapted Semantic Versioning system. By leveraging Mermaid diagrams, complex versioning concepts are broken down into intuitive and easily digestible visual formats, facilitating better comprehension and application.

### Key Highlights:
- **Clear Structure:** Diagrams illustrate the hierarchical components of the version number, ensuring clarity in understanding each segment's purpose.
- **Incrementing Rules:** Flowcharts guide the appropriate version increments based on the nature of changes, promoting consistency and predictability.
- **Precedence Comparison:** Visual representations aid in grasping how different versions relate to each other in terms of precedence.
- **Workflow Visualization:** The versioning workflow diagram encapsulates the entire lifecycle from initial development to maintenance, providing a holistic view.
- **Grammar Representation:** BNF diagrams translate the formal grammar rules into visual formats, bridging the gap between theoretical specifications and practical understanding.

### How to Use These Diagrams:
1. **Reference During Development:** Utilize the diagrams as a reference to determine when and how to increment version numbers based on the changes introduced.
2. **Educate Team Members:** Share the documentation with your development team to ensure a unified understanding of the versioning strategy.
3. **Integrate into Documentation:** Embed these diagrams within your project's documentation to provide clear guidelines for contributors and stakeholders.
4. **Automate Versioning Processes:** Leverage the incrementing rules flowchart to automate version bumps within your CI/CD pipelines, ensuring adherence to the versioning scheme.

### Future Enhancements:
- **Interactive Diagrams:** Consider making the diagrams interactive for enhanced user engagement and exploration.
- **Extended Examples:** Incorporate more real-world scenarios and examples to further elucidate the versioning principles.
- **Integration with Tools:** Explore integrations with versioning tools and plugins that can generate or validate version numbers based on the documented rules.

By adhering to the **Semantic Versioning 3.0.0_0** framework and utilizing the accompanying Mermaid diagrams, projects can achieve a more structured, transparent, and scalable approach to version management, ultimately contributing to smoother development cycles and more reliable software releases.
