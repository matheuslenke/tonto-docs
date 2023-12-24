---
id: intro
sidebar_position: 1
---

# Introduction

![Tonto Logo](/img/tonto-full-logo.png)

The original paper that presented Tonto can be found [here.](https://ufesbr-my.sharepoint.com/personal/cienciadacomputacao_ufes_br/_layouts/15/onedrive.aspx?ga=1&id=%2Fpersonal%2Fcienciadacomputacao%5Fufes%5Fbr%2FDocuments%2FTCCs%2F2023%2FMatheus%20Lenke%20Coutinho%20%2D%20Tonto%20A%20Textual%20Language%20for%20Ontology%2DDriven%20Conceptual%20Modeling%2Epdf&parent=%2Fpersonal%2Fcienciadacomputacao%5Fufes%5Fbr%2FDocuments%2FTCCs%2F2023)

Tonto is an acronym with the words Textual and Ontology, because it is a written way of writing Ontology models. It was developed using the Langium tool, with Typescript, and creates a Visual Studio Code Extension with a Language server.

Tonto was designed as a friendly textual syntax for ontologies. It offers specialized support for constructs reflecting the UFO foundational ontology, which makes it possible to identify errors in the ontology that would otherwise pass unnoticed. The language was designed to allow transformation to a number of languages including UML (more specifically OntoUML), OWL (for gUFO-based ontologies), Alloy, Common Logic, and the TPTP syntax.

The language supports:

* UFO-based annotations to facilitate error checking and meaning negotiation

* High-order types for multi-level taxomies

<!-- Structured comments for documentation generation -->

<!-- Constraints specification when extra precision is required -->

* Ontology testing/verification directives

As a textual syntax, the language can benefit from source control tools such as git, and ontologies can be viewed and edited without special tools. This VS Code extension is provided with support for syntax verification, syntax highlight, content assist and ontology visualization preview. The extension is integrated with the OntoUML server, to benefit from services designed for the language, such as transformation to OWL and generation of database schemas.
