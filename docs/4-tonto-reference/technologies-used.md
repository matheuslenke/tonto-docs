---
id: tonto-technologies-used
description: Technologies used for the creation of Tonto
sidebar_position: 1
---

# Technologies Used

The source code of Tonto can be found on its [GitHub repository](https://github.com/matheuslenke/Tonto)

## Langium

[**Langium**](https://langium.org/) is an open-source tool developed by TypeFox with first-class support for the Language Server Protocol (LSP). It utilizes TypeScript and runs on the Node.js runtime. With Langium, it is possible to develop textual Domain Specific Languages (DSLs) that can be used in IDEs such as VS Code, Eclipse Theia, and also in Web applications.

The tool generates a typed Abstract Syntax Tree (AST) along with default implementations for many LSP features. Thus, it automatically generates extensions for VS Code based on the created DSL, enabling features such as auto-complete, syntax highlighting, validators, code generators, and the development of a command-line interface (CLI).

Being created by the same team that produced a widely popular similar tool (for the Eclipse world), Xtext, *Langium* is robust and aims to maintain the concepts that made Xtext successful while improving them for another platform in a simple and clear manner.

## Visual Studio Code

[**Visual Studio Code**](https://code.visualstudio.com/), also known as VS Code, is a source code editor available for Windows, Linux, and macOS, developed by Microsoft. It includes support for debugging, built-in git version control, syntax highlighting, intelligent code completion, snippets, and code refactoring. It is highly customizable, allowing users to modify themes, keyboard shortcuts, and various preferences, which can be synchronized across devices.

Although the base version of VS Code may not have support for certain languages and functionalities, it can be extended by installing extensions. With the help of extensions, it becomes a powerful programming tool and can be considered an Integrated Development Environment (IDE). The extensions assist in syntax highlighting, code formatting, adding new snippets, refactoring, code execution and debugging, version control, error visualization, and many other functionalities.

In this project, VS Code is essential as it executes the extension that enables the utilization of all Tonto features. The IDE also provides extensive support for extension development, along with rich and detailed online documentation.

## TypeScript and Node.js

[**TypeScript**](https://www.typescriptlang.org/) is a strongly typed programming language that is built on top of another programming language, JavaScript. It adds additional syntax to JavaScript to support error identification at compile time instead of runtime. TypeScript transpiles all its code to JavaScript, which allows it to run in any environment that supports JavaScript. In the case of this project, it is executed in the Node.js environment.

[**Node.js**](https://nodejs.org/en/) is an open-source, cross-platform JavaScript runtime environment. It was developed to execute JavaScript code beyond the browser, targeting current operating systems. Node.js is designed for building scalable network applications and is an asynchronous, event-driven runtime, allowing multiple connections to be executed concurrently. In this project, Node.js serves as the execution environment for Tonto as it runs within the Language Server of VS Code. Therefore, it is possible to leverage all the available APIs of Node.js if needed.

<!-- Next chapters -->
<!-- available-classes -->
<!-- relations stereotypes -->
<!-- tonto datatypes -->