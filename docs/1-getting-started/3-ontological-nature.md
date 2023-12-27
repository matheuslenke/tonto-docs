---
id: tonto-ontological-natures
description: Defining ontological Natures
sidebar_position: 3
---

# Ontological Natures

Aditionally, we have the possibility of declaring nature restrictions for elements in Tonto. Elements in OntoUML can have nature restrictions based on their stereotypes.
Due to the fact that ultimate sortals already have a nature restriction, they cannot specify any different nature. Other sortal stereotypes define their nature restriction based on the ultimate sortal it specializes, carrying the same nature.

Another option is to define nature restrictions explicitly in the class declaration.  This is useful when having non-sortal elements that can specify the nature of their instances (and the nature of their instances). One example could be a category named *Social Entity* that is restricted to functional complexes, and is specialized by the kind *Hospital*:

```bash
package TontoNatures

category SocialEntity of functional-complexes

kind Hospital specializes SocialEntity
```

In addition to OntoUML, Tonto adds a syntactic sugar for a nature called *of objects*, representing Substantial Endurants. It is a short syntax to declare the 3 natures of substantials: *functional complexes, collectives and quantities*.
