---
id: tonto-gensets
description: Add Generalization Sets to your Model
sidebar_position: 2
---

# Generalization Sets

Another important construct in OntoUML is a *Generalization set*, based on the same construct in UML. An association is formed between a general element and a group of its specializations through the use of a generalization set. They can be decorated with the keywords *disjoint* and *complete*. The first keyword indicates that each instance of the superclass can only instantiate a maximum of one of the subclasses. The second keyword defines scenarios where instances of the general class are required to instantiate at least one of the subclasses.

![Example 1 model](/img/diagrams/fig-diagrams-example1.png)

## Basic Declaration

Similarly to the direct specializations on the model in the last chapter, we could utilize generalization sets. Tonto generalization set syntax is based on ML2. At first, we have the Tonto short syntax implementation of this generalization set, being the simplest form to declare it and fitting in one line.

```bash
phase Child
phase Teenager
phase Adult

disjoint complete genset PhasesOfPerson where Child, Teenager, Adult specializes Person
```

## Full declaration

For better organization, it is also possible to define the elements of the generalization inside brackets:

```bash
phase Child
phase Teenager
phase Adult

disjoint complete genset PhasesOfPerson {
    general Person
    specifics Child, Teenager, Adult
}
```

## Full declaration with categorizer

Lastly, we can add a type as a categorizer of the generalization set. The type *PersonTypeByAge* is declared and can be used as a categorizer for this generalization set:

```bash
type PersonTypeByAge

phase Child
phase Teenager
phase Adult

disjoint complete genset PhasesOfPerson {
    general Person
    categorizer PersonTypeByAge
    specifics Child, Teenager, Adult
}
```

Great! Now you know how to declare generalization sets!
