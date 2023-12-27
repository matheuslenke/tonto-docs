---
id: vscode-validators
description: Test
sidebar_position: 1
---

# Tonto Validators

In this section, we will describe each validator implemented on Tonto LSP. Every validator runs in the context of a package automatically when there are changes in code. All validators were inspired by the ones developed at ontouml-js, with some changes due to differences between Tonto and JSON syntaxes.

## Ultimate Sortal specialization validator

This validator checks whether the class declaration is an Ultimate Sortal and whether it specializes other Ultimate sortals. Because ultimate sortals should not do this specialization, this shows an error as presented in the next figure.

![Tonto VSCode extension showing an error of the Ultimate sortal validator](/img/validators/fig-validators-ultimate-sortal.png)

## Sortal specializes more than one ultimate sortal validator

This validator checks whether the class declaration is a sortal and calculates how many ultimate sortals it specializes directly or indirectly, analyzing every element until the topmost one. If it specializes in more than one, it displays an error as shown in the next figure, informing the modeler that the class should specialize only one ultimate sortal.

![Tonto VSCode extension showing an error of the Sortal specializes Ultimate sortal validator](/img/validators/fig-validators-sortal-specializes-ultimatesortal.png)

## Sortal should specialize ultimate sortal validator

This validator checks whether a class declaration is a sortal and calculates how many ultimate sortals are specialized, similarly to the previous validator. If it does not specialize any, it shows an error that it should specialize one. In the next figure we can see an example of this error.

![Tonto VSCode extension showing an error of the sortal should specialize ultimate sortal validator.](/img/validators/fig-validators-sortal-missing-specialization-nature.png)

## Rigid specializes Anti-rigid validator

This validator verifies whether, in a generalization between two classes, the general class has an Anti-rigid stereotype and the specific class has a rigid or semi-rigid stereotype, showing an error like in the next figure if that is the case.

![Tonto VSCode extension showing an error of Rigid element specializing Anti-rigid validator.](/img/validators/fig-validators-rigid-specializes-antirigid.png)

## Compatible Natures of sortals validator

 This validator verifies whether the class declaration is a (non-kind) base sortal (subkind, phase, role, historicalRole) and whether it defines a nature for its instances. The nature can be defined explicitly with tonto grammar, or it could be inherited from specialized classes. It shows an error when a nature specification is missing. For example, *subkind Customer* should specialize an ultimate sortal like *kind Person*.The next figure shows an example of this error.

![Tonto VSCode extension showing an error of the Compatible natures of sortals validator.](/img/validators/fig-validators-nature-situations.png)

## Compatible Natures validator

This validator verifies if non-sortals or base sortals specialize incompatible natures based on elements that it specializes in. For example, if a class is declared as *role Customer of objects} and it specializes in the kind *Person*, it should have an error like in the following figure

![Tonto VSCode extension showing an error of the Compatible Natures validator](/img/validators/fig-validators-incompatible-nature-objects.png)

## Redundant Natures

This validator verifies if an explicit declaration of nature is redundant for the element. This happens for ultimate sortals that already have a defined nature and cannot specialize other natures. Also, this happens for cases when a sortal or non-sortal inherits its nature from an ultimate sortal and tries to explicitly define the same nature when that is not needed. On the following figure we have two examples: the first is a kind, that already have the nature of functional complexes, so there is no need to specify it, and an example of a role Student that already have its nature defined by specializing the kind *Person*, with no need to specify again the nature of functional complexes.

![Tonto VSCode extension showing a warning of the Redundant Natures validator](/img/validators/fig-validators-redundant-natures.png)

## Other validators

Lastly, we defined other smaller validators to ensure code quality of the model:

- **Class without more specific keywords:** This validator shows a warning if an element is declared using the keyword **class** and do not provide any nature.

- **Check duplicates:** This validator checks for duplicate names of class declarations, relations, datatypes, and attributes.

- **Check circular specialization:** This validator checks whether an element with specializations does not have a cyclic specialization.
