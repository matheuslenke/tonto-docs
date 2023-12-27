---
id: tonto-package-manager
description: Test
sidebar_position: 7
---

# Tonto Package Manager

With Langium and VSCode Extension, it is possible to create powerful Tonto projects with many files and packages, allowing the definition of large models. However, a great way developed in popular programming languages is the possibility to encapsulate code as a package to be distributed and reused on other projects, some of them being open-source, with its source code available for everyone. This was one of the reasons for the increasing development speed in many companies doing software development. Tonto Package Manager (TPM) was created to provide the same capabilities for Tonto. TPM is based on popular solutions, for example, NPM (Node Package Manager), SPM (Swift Package Manager) and Cargo, the package managers for JavaScript, Swift, and Rust, respectively.

As a consequence of Package Managers being complex projects requiring a lot of effort to build every function, some decisions were made to simplify this task in our context. First, every project must be hosted on a git repository, with the possibility of defining a directory that the package is relative to the root folder, a version tag published on the repository, or a branch in case it is different from the main branch. Also, no *lock file* is created to manage current versions installed of dependencies, unlike the mentioned package manager npm. Because there is no complex code compilation, this file is not required in Tonto. Finally, every Tonto dependency is downloaded to a folder named *tonto\_dependencies* that must not be uploaded to code versioning tools like git.

## Manifest File

In order to be able to identify a project and its dependencies, a package manifest file is needed to be defined. A package manifest file is a file containing every piece of information required to make it complete and to distribute it for other projects to use. In Tonto, the manifest file must be named **tonto.json** and is defined in a JSON format with a correct definition of key-value properties. The following code provides an example of a manifest file for the University Example. One possibility of dependency defined is for the CoreDatatypes package, which could be a separate package.

```text
{
  "projectName": "UniversityModel",
  "displayName": "University Model",
  "authors": ["Matheus Lenke Coutinho"],
  "license": "MIT",
  "version": "1.0.0",
  "publisher": "UFES",
  "dependencies": {
    "CoreDataTypes": {
      "url": "https:github.com/url-to-package",
      "directory": "path/to/package"
    }
  },
  "outFolder": "out"
}
```
