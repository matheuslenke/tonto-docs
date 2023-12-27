---
id: theory-ontouml-as-service
description: OntoUML as a Service features
sidebar_position: 4
---

# OntoUML as a service

With the base theory, a group of tools were developed to support the development of UFO-based models through OntoUML using microsservices. This group of tools is called *OntoUML as a Service infrastructure (OaaS)*.
They were developed by Claudenir M. Fonseca, Tiago Prince Sales, Victor Viola, Lucas B. R. da Fonseca, Giancarlo Guizzardi and João Paulo A. Almeida and the original paper can be found [here](https://nemo.inf.ufes.br/wp-content/papercite-data/pdf/ontology_driven_conceptual_modeling_as_a_service_2021.pdf).

This infrastucture includes:

- [**ontouml-js:**](https://github.com/OntoUML/ontouml-js) A library developed in TypeScript that allows the creation and serialization of OntoUML models using JavaScript methods.

- [**ontouml-schema:**](https://github.com/OntoUML/ontouml-schema) A JSON schema that defines a set of rules to how OntoUML models are serialized in this format.

- [**ontouml-server:**](https://github.com/OntoUML/ontouml-server) An HTTP server created to provide validation and transformation features to OntoUML models in JSON format. The validation service takes in a serialized JSON model, applies syntactic validations to it, and if there are any errors, it returns an array of those errors, otherwise it return that the model is valid. The transformation service transforms a serialized JSON model into gUFO-based OWL ontologies.

- [**ontouml-vp-plugin:**](https://github.com/OntoUML/ontouml-vp-plugin) A plugin for the Visual Paradigm tool created originally for UML. The plugin offers a range of helpful features that allow the modeler to visualize OntoUML constructs with ease and modify them. Additionally, the plugin is designed to connect with ontouml-server, providing users with validation and transformation capabilities.
