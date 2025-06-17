# Semantic Versioning 3.0.0_0 (Adapted from Semantic Versioning 2.0.0)

## Summary

This document presents the adapted version of Semantic Versioning, transitioning from the original 2.0.0 specification to a four-digit system, designated as Semantic Versioning 3.0.0_0. This adaptation introduces a `RELEASE` identifier and modifies delimiters to enhance clarity and scalability in version management.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Version Number Format](#version-number-format)
3. [Semantic Versioning Specification (SemVer) 2.0.0](#semantic-versioning-specification-semver-200)
4. [Adapted Semantic Versioning Specification](#adapted-semantic-versioning-specification)
5. [Why Use Semantic Versioning?](#why-use-semantic-versioning)
6. [FAQ](#faq)
7. [Backus–Naur Form Grammar for Valid SemVer Versions](#backus–naur-form-grammar-for-valid-semver-versions)
8. [Adapted Backus–Naur Form (BNF) Grammar](#adapted-backus–naur-form-bnf-grammar)
9. [Usage Guidelines](#usage-guidelines)
10. [Regular Expression for Validation](#regular-expression-for-validation)
11. [Benefits of the Adapted System](#benefits-of-the-adapted-system)
12. [Versioning Rules and Increment Guidelines](#versioning-rules-and-increment-guidelines)
13. [Detailed Examples](#detailed-examples)
14. [Precedence and Comparison Rules](#precedence-and-comparison-rules)
15. [Notes and Best Practices](#notes-and-best-practices)
16. [Conclusion](#conclusion)
17. [Additional Resources](#additional-resources)
18. [License](#license)

---

## Introduction

In the realm of software development, effective version management is crucial to maintain compatibility and manage dependencies. Semantic Versioning (SemVer) provides a standardized approach to version numbering, conveying meaning about the underlying changes in a release.

**Semantic Versioning 3.0.0_0** adapts the original SemVer 2.0.0 to a four-digit system, introducing a `RELEASE` identifier to better manage pre-release versions and build metadata. This adaptation aims to enhance clarity, flexibility, and scalability in version management, addressing the evolving needs of modern software projects.

---

## Version Number Format

MAJOR.MINOR.PATCH_RELEASE+METADATA

- **MAJOR**: Indicates incompatible API changes.
- **MINOR**: Denotes the addition of functionality in a backward-compatible manner.
- **PATCH**: Represents backward-compatible bug fixes.
- **RELEASE**: Signifies pre-release identifiers (e.g., alpha, beta, rc).
- **METADATA**: Contains build metadata for additional context.

**Example:** `1.2.3_0+build.456`

---

## Semantic Versioning Specification (SemVer) 2.0.0

*Original Source Documentation*

Semantic Versioning 2.0.0 defines a versioning scheme with three numeric identifiers (MAJOR.MINOR.PATCH) and optional pre-release and build metadata.

### Key Points:

1. **MAJOR** version when you make incompatible API changes.
2. **MINOR** version when you add functionality in a backward-compatible manner.
3. **PATCH** version when you make backward-compatible bug fixes.
4. **Pre-release** versions denoted by a hyphen (`-`).
5. **Build metadata** denoted by a plus sign (`+`).

For detailed specifications, refer to [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).

---

## Adapted Semantic Versioning Specification

### 1. Version Number Structure

A version number consists of **MAJOR**, **MINOR**, **PATCH**, and **RELEASE** identifiers, with optional **METADATA**:

```
MAJOR.MINOR.PATCH_RELEASE+METADATA
```

- **MAJOR**, **MINOR**, **PATCH**: Non-negative integers without leading zeros.
- **RELEASE**: Alphanumeric identifiers separated by dots (`.`), following an underscore (`_`).
- **METADATA**: Alphanumeric identifiers separated by dots (`.`), following a plus sign (`+`).

### 2. Incrementing Rules

1. **MAJOR Version (`MAJOR`):**
   - **Increment When:** Incompatible API changes.
   - **Effect:** Resets `MINOR`, `PATCH`, and `RELEASE` to `0`.
   - **Example:** `1.4.5_2` → `2.0.0_0`

2. **MINOR Version (`MINOR`):**
   - **Increment When:** Adding functionality in a backward-compatible manner.
   - **Effect:** Resets `PATCH` and `RELEASE` to `0`.
   - **Example:** `1.4.5_2` → `1.5.0_0`

3. **PATCH Version (`PATCH`):**
   - **Increment When:** Making backward-compatible bug fixes.
   - **Effect:** Resets `RELEASE` to `0`.
   - **Example:** `1.4.5_2` → `1.4.6_0`

4. **RELEASE Identifier (`RELEASE`):**
   - **Increment When:** Releasing pre-release versions (e.g., alpha, beta, rc).
   - **Effect:** Can be incremented to denote new pre-release iterations.
   - **Example:** `1.4.5_0` → `1.4.5_1` (e.g., `alpha.1`)

5. **METADATA (`METADATA`):**
   - **Append When:** Including build information or other metadata.
   - **Example:** `1.4.5_1+build.123`

### 3. Pre-Release and Build Metadata

- **Pre-Release (`RELEASE`):**
  - Denoted by appending an underscore followed by pre-release identifiers.
  - Examples: `1.0.0_alpha`, `2.1.3_beta.1`, `3.0.0_rc.2`

- **Build Metadata (`METADATA`):**
  - Denoted by appending a plus sign followed by build identifiers.
  - Examples: `1.0.0_alpha+build.001`, `2.1.3_beta.1+exp.sha.5114f85`

### 4. Precedence Rules

Version precedence is determined by comparing each identifier from left to right:

1. **MAJOR**, **MINOR**, and **PATCH** are compared numerically.
2. **RELEASE** identifiers are compared:
   - Absence of a pre-release (`RELEASE`) signifies higher precedence.
   - When present, they are compared lexically and numerically.
3. **METADATA** does not affect precedence.

**Examples:**
- `1.0.0_alpha < 1.0.0`
- `1.0.0_alpha < 1.0.0_beta`
- `1.0.0_beta < 1.0.0_beta.1`
- `1.0.0_beta.1 < 1.0.0_beta.2`

---

## Why Use Semantic Versioning?

Semantic Versioning provides a clear and consistent way to communicate changes in software versions, facilitating better dependency management and reducing the risks associated with version mismatches. By adopting Semantic Versioning 3.0.0_0, projects can enhance their versioning strategy to accommodate more detailed release information, improving clarity and scalability.

---

## FAQ

### How should I deal with revisions in the 0.y.z initial development phase?

Start your initial development release at `0.1.0_0` and increment the minor version for each subsequent release.

### How do I know when to release 1.0.0_0?

Transition to `1.0.0_0` once your software is stable and ready for production use, with a well-defined public API.

### Doesn’t this discourage rapid development and fast iteration?

No. The `RELEASE` identifier (`_0`, `_1`, etc.) allows for rapid iteration during development phases without altering the core version numbers.

### If even the tiniest backward incompatible changes to the public API require a major version bump, won’t I end up at version 42.0.0_0 very rapidly?

Responsible development and foresight prevent unnecessary major version increments. Incompatible changes should be introduced judiciously.

### Documenting the entire public API is too much work!

Proper documentation is essential for managing software complexity and ensuring usability. Semantic Versioning encourages clear communication of changes.

### What do I do if I accidentally release a backward incompatible change as a minor version?

Release a new major version to correct the mistake and inform your users of the issue.

### What should I do if I update my own dependencies without changing the public API?

Consider it a patch or minor update based on whether the changes introduce new functionality or fix bugs.

### What if I inadvertently alter the public API in a way that is not compliant with the version number change?

Use your best judgment to perform a major version release to inform users of significant changes.

### How should I handle deprecating functionality?

Update your documentation and issue a new minor release with deprecations in place, followed by a major release to remove deprecated features.

### Does SemVer have a size limit on the version string?

No, but it's advisable to keep version strings concise and within reasonable lengths.

### Is “v1.2.3_0” a semantic version?

Yes, `v1.2.3_0` follows the adapted Semantic Versioning 3.0.0_0 format, indicating a release with a `RELEASE` identifier.

### Is there a suggested regular expression (RegEx) to check a SemVer string?

Yes, see the [Regular Expression for Validation](#regular-expression-for-validation) section below.

---

## Backus–Naur Form Grammar for Valid SemVer Versions

*Original Source Documentation*

`````
### **Adapted Backus–Naur Form (BNF) Grammar**

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
`````

---

## Adapted for `SemVer 3.0.0_0` - Backus–Naur Form (BNF) Grammar

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

## Usage Guidelines

1. **Initial Development:**
   - Start with `0.1.0_0`
   - Increment the **MINOR** version for each new iteration within initial development.
   - Example: `0.1.0_0` → `0.2.0_0` → `0.3.0_0`

2. **Releasing MVP:**
   - Transition to `1.0.0_0` once the MVP is ready.
   - **MAJOR** version is incremented when moving from initial development to MVP.
   - Example: `0.3.0_0` → `1.0.0_0`

3. **Pre-Release Stages:**
   - Use the **RELEASE** identifier to denote pre-release stages.
   - Example: `1.0.0_0_alpha`, `1.0.0_0_beta.1`

4. **Final Release:**
   - After successful testing, release the final version.
   - Example: `1.0.0_0_beta.2` → `1.0.0_0+build.789`

5. **Maintenance:**
   - Increment the **MAJOR** version for significant updates.
   - Increment the **MINOR** version for minor feature additions.
   - Increment the **PATCH** version for bug fixes.
   - Example: `1.0.0_0+build.789` → `1.1.0_0+build.790` → `1.1.1_0+build.791`

---

## Regular Expression for Validation

To validate the adapted versioning system, use the following regular expression:

```plaintext
^(0|[1-9]\d*)\.(0|[1-9]\d*)\.(0|[1-9]\d*)_(0|[1-9]\d*)(?:-((?:0|[1-9]\d*|\d*[a-zA-Z-][0-9a-zA-Z-]*)(?:\.(?:0|[1-9]\d*|\d*[a-zA-Z-][0-9a-zA-Z-]*))*))?(?:\+([0-9a-zA-Z-]+(?:\.[0-9a-zA-Z-]+)*))?$
```

**Explanation:**
- **MAJOR, MINOR, PATCH:** Numeric identifiers without leading zeros.
- **RELEASE:** Numeric identifier following an underscore (`_`).
- **Pre-Release:** Optional, denoted by a hyphen (`-`) followed by identifiers.
- **Build Metadata:** Optional, denoted by a plus sign (`+`) followed by identifiers.

---

## Benefits of the Adapted System

- **Clarity:** Clear distinction between different stages of development and release.
- **Flexibility:** Ability to append metadata for build information without affecting version precedence.
- **Consistency:** Maintains the integrity of Semantic Versioning principles while adapting to a four-digit format.
- **Scalability:** Easily accommodates future expansions and modifications without disrupting existing versioning logic.

---

## Versioning Rules and Increment Guidelines

| **Action**                                     | **Component to Increment** | **Resulting Change**                              | **Example Transition**          |
|------------------------------------------------|----------------------------|---------------------------------------------------|---------------------------------|
| **Incompatible API Changes**                   | MAJOR                      | Increment MAJOR, reset MINOR, PATCH, RELEASE to 0  | `1.1.1_1` → `2.0.0_0`           |
| **Adding Backward-Compatible Functionality**   | MINOR                      | Increment MINOR, reset PATCH and RELEASE to 0      | `1.0.0_0` → `1.1.0_0`           |
| **Backward-Compatible Bug Fixes**             | PATCH                      | Increment PATCH, reset RELEASE to 0                | `1.1.0_0` → `1.1.1_0`           |
| **Pre-Release (e.g., Alpha, Beta, RC)**        | RELEASE                    | Increment RELEASE identifier                       | `1.0.0_0` → `1.0.0_1`           |
| **Appending Build Metadata**                   | Metadata                   | Append metadata after `+`                          | `1.0.0_1` → `1.0.0_1+build.123` |
| **Major Update with Build Metadata**           | MAJOR + Metadata           | Increment MAJOR, reset others, append metadata     | `2.1.1_1` → `3.0.0_0+build.789` |
| **Minor Update with Build Metadata**           | MINOR + Metadata           | Increment MINOR, reset others, append metadata     | `1.1.0_0` → `1.1.0_1+build.456` |
| **Patch Update with Build Metadata**           | PATCH + Metadata           | Increment PATCH, reset RELEASE, append metadata    | `1.1.1_0` → `1.1.1_1+build.101` |

---

## Detailed Examples

| **Scenario**                                | **Current Version** | **Action**                               | **New Version**          | **Notes**                                            |
|---------------------------------------------|---------------------|------------------------------------------|--------------------------|------------------------------------------------------|
| **Initial Development Start**              | `0.0.0_0`           | Start prototyping                        | `0.1.0_0`                | Increment MINOR for initial feature additions.       |
| **Alpha Pre-Release**                       | `0.1.0_0`           | Release alpha version internally         | `0.1.0_1`                | Increment RELEASE identifier for alpha release.      |
| **Bug Fix in Prototype Phase**             | `0.1.0_1`           | Fix bug                                  | `0.1.1_0`                | Increment PATCH for bug fix, reset RELEASE to 0.      |
| **MVP Launch**                              | `0.1.1_0`           | Transition to MVP                         | `1.0.0_0`                | Increment MAJOR for MVP release, reset others to 0.   |
| **Adding New Feature to MVP**               | `1.0.0_0`           | Add new backward-compatible feature       | `1.1.0_0`                | Increment MINOR for new feature addition.             |
| **Internal Alpha Release Post-MVP**         | `1.1.0_0`           | Release internal alpha                    | `1.1.0_1`                | Increment RELEASE for internal alpha testing.        |
| **External Beta Release**                   | `1.1.0_1`           | Release external beta                      | `1.1.0_2`                | Increment RELEASE for external beta testing.         |
| **Bug Fix in Beta Phase**                   | `1.1.0_2`           | Fix bug in beta                           | `1.1.1_0`                | Increment PATCH for bug fix, reset RELEASE to 0.      |
| **Final Production Deployment**             | `1.1.1_0`           | Deploy to production                       | `1.1.1_1+build.123`      | Append metadata for build tracking.                  |
| **Major Release with Incompatible Changes** | `1.1.1_1+build.123` | Introduce incompatible API changes        | `2.0.0_0+build.456`      | Increment MAJOR, reset others, append new metadata.   |
| **Maintenance Feature Addition**            | `2.0.0_0+build.456` | Add new feature during maintenance        | `2.1.0_0+build.456`      | Increment MINOR, retain build metadata.               |
| **Maintenance Bug Fix**                     | `2.1.0_0+build.456` | Fix bug in maintenance                    | `2.1.1_0+build.456`      | Increment PATCH, retain build metadata.              |
| **Maintenance Release with Metadata**       | `2.1.1_0+build.456` | Release maintenance build with metadata  | `2.1.1_1+build.789`      | Increment RELEASE for maintenance build, append metadata.|

---

## Precedence and Comparison Rules

| **Version A**       | **Version B**         | **Relationship**                          | **Reason**                                               |
|---------------------|-----------------------|-------------------------------------------|----------------------------------------------------------|
| `1.0.0_0`           | `1.0.0_1`             | `<`                                       | `RELEASE` identifier `0` < `1`                           |
| `1.0.0_1`           | `1.0.0_1+build.001`   | `=`                                       | Metadata does not affect precedence                      |
| `1.0.0_1`           | `1.0.0_2`             | `<`                                       | `RELEASE` identifier `1` < `2`                           |
| `1.1.0_0`           | `1.1.0_0+build.002`   | `=`                                       | Metadata does not affect precedence                      |
| `1.1.0_0`           | `1.1.1_0`             | `<`                                       | `PATCH` version `0` < `1`                                |
| `2.0.0_0`           | `1.1.1_0`             | `>`                                       | `MAJOR` version `2` > `1`                                 |
| `2.0.0_0`           | `2.0.0_1`             | `<`                                       | `RELEASE` identifier `0` < `1`                           |
| `2.0.0_1`           | `2.0.0_1+build.004`   | `=`                                       | Metadata does not affect precedence                      |
| `2.1.0_0`           | `2.1.0_1`             | `<`                                       | `RELEASE` identifier `0` < `1`                           |
| `3.0.0_0`           | `2.1.1_0`             | `>`                                       | `MAJOR` version `3` > `2`                                 |
| `3.0.0_0+build.006` | `3.0.0_0+build.007`   | `=`                                       | Metadata does not affect precedence                      |

---

## Notes and Best Practices

1. **Consistent Incrementation:**
   - Always follow the incrementation rules to maintain versioning consistency.
   
2. **Metadata Usage:**
   - Use metadata to track build numbers, commit hashes, or other build-related information without altering version precedence.
   
3. **Pre-Release Identifiers:**
   - Utilize `RELEASE` identifiers (`_1`, `_2`, etc.) to manage pre-release versions like alpha, beta, and release candidates.
   
4. **Avoid Skipping Numbers:**
   - Increment version numbers sequentially to preserve clarity and predictability.
   
5. **Documentation:**
   - Clearly document the versioning scheme in your project’s README or documentation to ensure all stakeholders understand the versioning logic.
   
6. **Automate Versioning:**
   - Implement scripts or tools within your CI/CD pipeline to automate version number increments based on commit messages or merge actions.

---

## Conclusion

By adapting the Semantic Versioning 2.0.0 principles to a four-digit system with an underscore delimiter (`_`), Semantic Versioning 3.0.0_0 maintains the robustness and clarity of version management while aligning with specific formatting requirements. This system ensures that version numbers convey meaningful information about the nature of changes, facilitating better dependency management and reducing the risks associated with version mismatches.

**Key Takeaways:**
- **MAJOR.MINOR.PATCH_RELEASE+METADATA:** The core structure adapted for a four-digit system.
- **Increment Rules:** Clear guidelines for when and how to increment each part of the version number.
- **Metadata Handling:** Seamless integration of build metadata without affecting version precedence.
- **Validation:** Regular expressions to ensure version numbers adhere to the defined format.

Implementing Semantic Versioning 3.0.0_0 enhances your project's maintainability, scalability, and interoperability, ensuring a smooth development and deployment lifecycle.

---

## Additional Resources

- **Semantic Versioning Official Website:** [https://semver.org/](https://semver.org/)
- **Semantic Versioning Specification (Adapted):** As detailed above.
- **Version Control Tools:**
  - [Git Documentation](https://git-scm.com/doc)
  - [GitHub Releases](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases)
- **Continuous Integration Tools:**
  - [Jenkins](https://www.jenkins.io/doc/)
  - [Travis CI](https://travis-ci.org/)
  - [CircleCI](https://circleci.com/)
- **Regular Expression Testing:**
  - [Regex101](https://regex101.com/) – Test and debug your regular expressions.

---

## License

[Creative Commons ― CC BY 3.0](https://creativecommons.org/licenses/by/3.0/)


---

### **Changes and Reasoning**

1. **Introduction of `RELEASE` Identifier:**
   - **Change:** Added `RELEASE` as the fourth component in the version number, separated by an underscore (`_`).
   - **Reasoning:** To better manage pre-release versions and provide more granularity in versioning, enhancing clarity and flexibility.

2. **Delimiter Modification:**
   - **Change:** Changed the delimiter between `PATCH` and `RELEASE` from a hyphen (`-`) to an underscore (`_`).
   - **Reasoning:** Differentiates between pre-release identifiers and the core version numbers, reducing confusion and improving readability.

3. **Incrementing Rules Adjustment:**
   - **Change:** Updated the incrementing rules to accommodate the new `RELEASE` identifier.
   - **Reasoning:** Ensures that each component of the version number is appropriately managed, maintaining consistency and predictability.

4. **Regular Expression Update:**
   - **Change:** Provided a new regular expression tailored to validate the adapted four-digit versioning system.
   - **Reasoning:** Facilitates automated validation of version numbers, ensuring adherence to the new format.

5. **Enhanced Usage Guidelines:**
   - **Change:** Expanded the usage guidelines to include examples specific to the adapted versioning system.
   - **Reasoning:** Offers clearer instructions for developers to implement the new versioning scheme effectively.

6. **Detailed Examples Expansion:**
   - **Change:** Added more comprehensive examples illustrating various version transitions within the adapted system.
   - **Reasoning:** Provides practical scenarios to aid understanding and application of the new versioning rules.

7. **Precedence Rules Clarification:**
   - **Change:** Updated the precedence rules to align with the introduction of the `RELEASE` identifier.
   - **Reasoning:** Maintains logical version comparison, ensuring that the adapted system preserves the intent of Semantic Versioning.

8. **Additional Sections Inclusion:**
   - **Change:** Included sections like "Benefits of the Adapted System" and "Versioning Rules and Increment Guidelines."
   - **Reasoning:** Enhances the documentation by highlighting the advantages of the adapted system and providing clear guidelines for implementation.

---

### **Suggested Reasoning Statement**

The adaptation of Semantic Versioning to a four-digit system with a `RELEASE` identifier (`Semantic Versioning 3.0.0_0`) addresses the need for more detailed version management in complex software projects. By introducing the `RELEASE` component and modifying delimiters, the system gains enhanced clarity and flexibility, facilitating better handling of pre-release stages and build metadata. These changes maintain the foundational principles of Semantic Versioning while providing scalability for future development needs, thereby improving dependency management and overall project maintainability.

---

This is merely an opinionated invtation for consideration, by @thedavidyoungblood from @louminailabs.
