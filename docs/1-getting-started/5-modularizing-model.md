---
id: tonto-modularizing
description: Test
sidebar_position: 5
---

# Modularizing your project

A Tonto project consists of all Tonto files opened in your workspace, automatically. Due to that fact, by default every
Tonto project is already modularized, the only effort needed is to create different files for each package.

The first step to modularize our University model could be creating a package for our custom datatypes called CoreDatatypes.
Create a new file called `CoreDatatypes.tonto`, and extract the code from the PersonPhases package:

```text
package CoreDatatypes

datatype PhoneNumber {
  countryCode: int [1]
  bodyNumber: int [1]
}

datatype int specializes number

enum EyeColor {
  Blue,
  Green,
  Brown,
  Black
}
```

In order to make our model work again, we need to go back to the PersonPhases package and add an import for our datatypes:

```bash
import CoreDatatypes

package PersonPhases
// Rest of package content...
```

In addition, we can go back to the University model, and create its own package instead of using the PersonPhases package
for its declaration.

![Example model in OntoUML of an University](/img/diagrams/fig-diagrams-example2.png)

In Tonto, we have:

```bash
import CoreDatatypes
import PersonPhases
package University

category Organization
kind University specializes Organization {
  address: Address
  @componentOf
  [1] <>-- has -- [1..*] Department
  @componentOf
  [1] <>-- [0..*] Classroom
}

relation Department [1] <>-- [1] JuniorStaff

kind Department {
  name: string
}
collective Staff
subkind JuniorStaff specializes Staff

kind Room
subkind Classroom specializes Room

subkind SeniorStaff specializes Staff

roleMixin Employer

role UniversityEmployer specializes Employer, University
```
