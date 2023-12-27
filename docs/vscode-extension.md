---
id: intro-installling
description: Installing Tonto Toolkit
sidebar_position: 2
---

# Installing

## Visual Studio Code Extension

The VS Code extension can be found at the extensions marketplace [here](https://marketplace.visualstudio.com/items?itemName=Lenke.tonto).

By using [Langium](https://langium.org), we could create a Language Server Protocol (LSP) and a Visual Studio Code extension for Tonto. The extension recognizes `.tonto` files and provides some key features to help with conceptual modeling. Every functionally needed to work with Tonto is embbeded in the extension, so there is no need to install any extra tool. However, in case you need it, the CLI and Package Manager are available as separate tools.

## Tonto CLI

To install Tonto CLI you need `Node.js` installed with a version `18.x` or higher. Tonto CLI works on Windows, Linux and MacOS. To install it globally on your environment, please run the following command:

```bash
    npm i -g tonto-cli
```

## Tonto Package Manager

Tonto Package Manager allows you to manage your models as libraries in common programming languages. It works simmilarly to Tonto CLI, and you can install it globally by running the following command:

```bash
    npm i -g tonto-package-manager
```
