---
id: vscode-features
description: An introduction to Tonto VS Code extension features
sidebar_position: 1
---

# Tonto VS Code Extension features

With Langium, a Language Server Protocol (LSP) is generated for a textual language, and a Visual Studio Code extension is created. The figure below shows the usage of this extension, demonstrating the University example. In VSCode, we open a directory that is the root of our workspace, and every file inside it is part of the project; similarly, the [Tonto extension](https://marketplace.visualstudio.com/items?itemName=Lenke.tonto) considers every file currently in the workspace with the `.tonto` extension to be part of the same project, with every file being a different package. Every file is automatically processed by the langium library, creating a LangiumDocument. This document goes through seven states, from parsing the AST to computing scopes, linking cross-references, doing validations, and then waiting for new changes.

![Example extension figure](/img/extension/fig-extension-1.png)

## Validation

The extension's first feature provides a way to visualize errors in the model because of the validators implemented automatically by Langium and those custom validators added to the extension based on OntoUML semantic rules. In the figure above, we have an example of the semantic error flagged by a custom validator. This error occurs because a class with the stereotype *role* must specialize one ultimate sortal, and  VScode also displays the error inline. This real-time visualization allows the modeler to spot errors in every new element added (without the need for special interventions such as clicking on a button).

## Commands

Another important feature is the commands available at the bottom of the editor and at the command palette. They are responsible for executing the same commands available for the Tonto CLI. From the first figure, we can see the following buttons:

- **Tonto -> JSON**: This generates a JSON from the model.
- **Tonto -> gUFO**: Validate the model with ontouml-server API.
- **JSON -> Tonto**: This generates a Tonto project from a JSON file.
- **Validate Model**: Validate the model with ontouml-server API.
- **TPM Install**: Install dependencies based on the Tonto Package Manager (TPM)

Every command automatically recognizes the workspace's root and executes from that directory. But, in some cases, it is needed to run a command in another directory in the same way provided by the CLI. In that case, they are available in the command palette and will ask the user to input the directory to be analyzed.

## Autocompletion and snippets

Finally, this extension enables the user with smart code completion and ready-to-use snippets that empower and fasten the development of models. Because of that feature, it is easy to get used to the syntax, and there is no need to write some boilerplate code that could slow development. An example of how code completion works:

![Example of extension Autocompletion](/img/extension/fig-extension-autocomplete.png)

The following figures shows an example of a list of snippets available for Tonto in the current context, and the usage of an internal relation snippet.

![Example of extension snippet](/img/extension/fig-extension-autocomplete.png)
![Example of extension snippet use](/img/extension/fig-extension-autocomplete.png)
