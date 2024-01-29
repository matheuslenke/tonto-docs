---
id: intro
sidebar_position: 1
---

# Introduction

![Tonto Logo](/img/tonto-full-logo.png)

The original paper that presented Tonto can be found [here.](https://matheuslenke.github.io/tonto-docs/pdf/Tonto.pdf) and the source code of Tonto can be found on its [GitHub repository](https://github.com/matheuslenke/Tonto)

Tonto is an acronym with the words Textual and Ontology, because it is a written way of writing Ontology models. It was developed using the Langium tool, with Typescript, and creates a Visual Studio Code Extension with a Language server.

Tonto was designed as a friendly textual syntax for ontologies. It offers specialized support for constructs reflecting the UFO foundational ontology, which makes it possible to identify errors in the ontology that would otherwise pass unnoticed. The language was designed to allow transformation to a number of languages including UML (more specifically OntoUML), OWL (for gUFO-based ontologies), Alloy, Common Logic, and the TPTP syntax.

The language supports:

* UFO-based annotations to facilitate error checking and meaning negotiation

* High-order types for multi-level taxomies

<!-- Structured comments for documentation generation -->

<!-- Constraints specification when extra precision is required -->

* Modularization of Models in multiple repositories

* Transformation to OWL-based implementation OntoUML tools

As a textual syntax, the language can benefit from source control tools such as git, and ontologies can be viewed and edited without special tools. This VS Code extension is provided with support for syntax verification, syntax highlight, content assist and ontology visualization preview. The extension is integrated with the OntoUML server, to benefit from services designed for the language, such as transformation to OWL and generation of database schemas.

![Tonto Example](/gif/1.gif)