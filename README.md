<h1>
    <a href="/#gh-light-mode-only">
        <img src="./assets/filo-logo-light-mode.svg#gh-light-mode-only" width=180>
    </a>
    <a href="/#gh-dark-mode-only">
        <img src="./assets/filo-logo-dark-mode.svg#gh-dark-mode-only" width=180>
    </a>
</h1>

Filo is a robust system designed to streamline folder management and organisation.

<div>
    <img src="https://img.shields.io/badge/Specification-gray.svg?style=flat-square" alt="Specification">
    <a href="https://opensource.org/license/gpl-3-0/">
        <img src="https://img.shields.io/badge/MIT-blue.svg?style=flat-square&label=License" alt="License = GNU GPL-3.0">
    </a>
    <img src="https://img.shields.io/badge/1.0.0-yellow.svg?style=flat-square&label=Version" alt="Version = 1.0.0">
</div>

## Table of Contents

- [Summary](#summary)
- [Introduction](#introduction)
- [Specification](#specification)
- [Backus–Naur Form Grammar](#backusnaur-form-grammar)
- [Why use Filo?](#why-use-filo)
- [FAQ](#faq)
- [License](#license)

## Summary

The Filo System is a hierarchical structure of folders with specially formatted names for each level:

- The Root folder is the "Documents" folder of the user's home directory.
- Domain, Facet, and Subject folders have names formatted like `[Code] Text`.
- Domain folders are below the Root. Their Codes are single-digit non-negative integers. E.g., "0" to "9".
- Facet folders are below Domain folders. Their Codes are double-digit non-negative integers comprising the parent Domain Code as a prefix before an arbitrary single-digit non-negative integer. E.g., "X0" to "X9", where "X" is the parent Domain Code.
- Subject folders are below Facet folders, or below other Subject folders. Their Codes comprise the parent Facet/Subject Code followed by a full-stop (".") character and then a zero-padded two-digit non-negative integer. E.g., "X.00" to "X.09", where "X" is the parent Facet or Subject Code.

When creating new folders, use the next available Code (from the front or the back), except for the Code which ends with "0" which may be reserved for metadata of the parent folder.

## Introduction

Filo is a system designed to streamline file management and organisation. This specification provides a comprehensive overview of the Filo system.

It aims to provide consistency, completeness, and simplicity in file management, while fostering good habits. The system encourages users to think critically about their file structure, promoting a personalised yet stable structure for organising documents. With the support of modern operating systems, users can quickly search their folders using memorised Filo Codes, enhancing efficiency and productivity.

The goals of the Filo system include:

1. **Consistency**: By using a unique identifier (Filo Code) for each Domain, Facet, and Subject, the system ensures a uniform structure across all files and folders.
2. **Completeness**: The system encompasses all aspects of a user's life, ensuring no area is left unorganised.
3. **Simplicity**: The Filo system is easy to use, with a clear and intuitive structure.
4. **Personalisation**: The concept of Domains and Facets allows users to create a system that is tailored to their needs.
5. **Futureproofing**: The system is designed to adapt and grow with the user, accommodating changes in their life and work.
6. **Efficiency**: With the ability to quickly search folders using Filo Codes, users can access their files faster than ever.

The Filo system's unique structure encourages users to use fewer 'levels' of folders, as the Subject Codes grow by three characters for each new level. This promotes a more streamlined and efficient organisation. Moreover, the Filo system is designed to adapt and grow with the user, accommodating changes in their life and work. This adaptability makes the system not only efficient but also resilient, capable of meeting the user’s needs now and in the future. In essence, the Filo system is more than just a file management tool; it’s a comprehensive solution for personal organisation and productivity.

## Specification

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in [RFC 2119](https://tools.ietf.org/html/rfc2119).

1. The set of all folders conforming to the below specification SHALL be known as the "**System**".
2. The folder which contains all other folders in the system SHALL be called the "**Root**". The Root SHOULD be the `Documents` folder of a user's home directory. Any given folder descendant to the Root MAY conform to the specification, those that do SHALL be called "**Filo Folders**", and those that do not SHALL be called "**Standard Folders**".
3. A Filo Folder directly descended from the Root SHALL be called a "**Domain**". A Domain MUST be associated with an identifier unique in the System which SHALL be called a "**Domain Code**". A Domain Code MUST be single-digit non-negative integer.
4. A Filo Folder directly descended from a Domain SHALL be called a "**Facet**". A Facet MUST be associated with an identifier unique in the System which SHALL be called a "**Facet Code**". A Facet Code MUST comprise the Domain Code of the parent Domain followed by a single-digit non-negative integer.
5. A Filo Folder directly descended from a Facet or another Subject SHALL be called a "**Subject**". A Subject MUST be associated with an identifier unique in the System which SHALL be called a "**Subject Code**". A Subject Code MUST comprise the Facet/Subject Code of the parent Facet/Subject, followed by a full stop character ("."), followed by a zero-padded two-digit non-negative integer.
6. Filo Folders MUST be named according to the format `[<code>] <text>`, where `<code>` is the associated unique identifier and `<text>` is a series of valid characters for a directory name. The RECOMMENDED characters to use for `<text>` are alphanumeric characters, full stops, dashes, underscores, and spaces.
7. Within a given Filo Folder, the complete list of Codes which directly descended Filo Folders may associate with SHALL be called the "**Possible Codes**" for that given Filo Folder. The subset of the Possible Codes which are not currently associated with Filo Folders SHALL be called the "**Available Codes**", the different between these two sets SHALL be called the "**Used Codes**". The single code in the Possible Codes set which ends with "0" in the case of Domains and Facets, or "00" in the case of Subjects, SHALL be called the "**Leading Code**".
8. Users MUST create a new Filo Folder using the next available Code. The next available Code MUST be determined numerically within a given Filo Folder, but the user MAY choose to order these available Codes ascending or descending. The user MAY reserve the Leading Code for storing metadata about the parent folder, i.e., remove the Leading Code from the set of Available Codes (should it not be in the set of Used Codes) when selecting the next code to use.

## Example

The following is an short example of a Filo System in action.

``` text
📁 Documents
├─ 📁 [0] System
├─ 📁 [1] Projects
│  ├─ 📁 [11] Programming
│  │  └─ 📁 [11.01] Filo
│  │     ├─ 📁 [11.01.00] Filo System Specification
│  │     └─ 📁 [11.01.01] Filo CLI
│  ├─ 📁 [12] Graphic design
│  └─ 📁 [13] Iconography
├─ 📁 [2] Work
├─ 📁 [3] Education
│  ├─ 📁 [31] High School
│  ├─ 📁 [32] University
│  │  ...
│  └─ 📁 [39] Certificates
├─ 📁 [4] Health
│  ...
└─ 📁 [9] Miscellaneous
```

## Backus–Naur Form Grammar

``` bnf
<valid filo folder name> ::= "[" <valid filo code> "]" <space> <generic text>

<valid filo code> ::= <domain code> | <facet code> | <subject code>

<domain code> ::= <digit>

<facet code> ::= <domain code> <digit>

<subject code> ::= <facet code> "." <double digit>
                 | <subject code> "." <double digit>

<generic text> ::= <alphanumeric extended>
         | <text> <alphanumeric extended>

<alphanumeric extended> ::= <letter> | <digit> | "-" | <space> | "_" | "."

<double digit> ::= <digit> <digit>

<digit> ::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"

<space> ::= " "

<letter> ::= "A" | "B" | "C" | "D" | "E" | "F" | "G" | "H" | "I" | "J"
           | "K" | "L" | "M" | "N" | "O" | "P" | "Q" | "R" | "S" | "T"
           | "U" | "V" | "W" | "X" | "Y" | "Z" | "a" | "b" | "c" | "d"
           | "e" | "f" | "g" | "h" | "i" | "j" | "k" | "l" | "m" | "n"
           | "o" | "p" | "q" | "r" | "s" | "t" | "u" | "v" | "w" | "x"
           | "y" | "z"
```

Please note, the `<alphanumeric_extended>` symbol is limited to letters, numbers, dashes, spaces, underscores, and full stops in this grammar; however, you may choose to extend this using any other characters you desire. The contents of the text in the folder name is not controlled by this specification, it is simply suggested that you limit yourself to these characters in folder names.

## Why use Filo?

Filo is more than just a file organisation system; it's a tool designed to streamline your digital life. With the exponential growth of digital data, managing files and folders can become a daunting task. Filo addresses this issue by providing a structured, yet flexible, system that adapts to your unique needs.

One of the key benefits of Filo is its simplicity. The system uses a hierarchical structure with unique identifiers (Filo Codes) for each Domain, Facet, and Subject. This makes it easy to locate files, reducing the time spent searching and increasing productivity. Whether you're a student juggling multiple assignments, a professional managing various projects, or simply someone trying to keep their digital life organised, Filo can help you stay on top of your game.

Filo also encourages good organisational habits. By limiting the number of Domains, Facets, and Subjects, the system nudges users towards broad categorisation, making it easier to memorise and locate files. This can be particularly beneficial for individuals who struggle with cluttered digital spaces.

Moreover, Filo is future-proof. The system is designed to grow with you, accommodating changes in your life and work. Whether you're starting a new job, pursuing further education, or picking up a new hobby, Filo can adapt to encompass all aspects of your life.

## FAQ

**Why should the Root folder be the Documents folder?**

The Root folder is recommended to be the Documents folder because it is a central location that is easily accessible on most operating systems. This helps in achieving the Filo system's goals of simplicity and efficiency. However, the choice of Root folder can be tailored to the user's needs, aligning with the goal of personalisation.

**Do I have to reserve the Leading Codes?**

Reserving the Leading Codes is optional and is recommended for storing metadata about the parent folder. This aligns with the goal of futureproofing the system by providing a designated place for additional information that may be needed in the future. However, if a user does not require this functionality, they can choose to use the Leading Codes for other purposes.

**Why do Facet Codes and Subject Codes need to use the parent folder Code as a prefix?**

Using the parent folder Code as a prefix for Facet Codes and Subject Codes ensures the uniqueness of each Code within the system, which aligns with the goal of consistency. It also helps in quickly identifying the hierarchical relationship between folders, contributing to the goal of simplicity. The increase in length is minimal (one or three characters) and is a trade-off for these benefits.

**What happens if I run out of Codes for a particular level (Domain, Facet, Subject)?**

If you run out of Codes for a particular level, it indicates that the current level has reached its maximum capacity. To maintain the simplicity and efficiency of the system, it is recommended to review your current structure and consider reorganising or consolidating some folders.

**Can I use Filo for managing files as well as folders?**

Filo is primarily designed for managing folders. However, you can extend its principles to file management if it suits your needs. This aligns with the goal of personalisation.

**Can I use Filo on any operating system?**

Yes, Filo is a system of organisation and can be used on any operating system that supports hierarchical file systems, which includes all major operating systems like Windows, macOS, and Linux.

**How does Filo handle cases where there are more than 10 Domains or Facets?**

Filo is designed to encourage broad categorisation. If you find you need more than 10 Domains or Facets, it may be a sign that you're categorising too narrowly. Consider consolidating similar Domains or Facets to maintain simplicity and efficiency.

**What happens if I want to move a Facet or Subject to a different Domain or Facet?**

Filo allows for flexibility, supporting the goal of futureproofing. If you need to move a Facet or Subject, you can do so, but remember to update the Code to reflect the new parent folder. This will maintain the consistency of the Filo system.

## License

This project is licensed under the [MIT License](LICENSE).
