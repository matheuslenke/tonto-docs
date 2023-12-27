---
id: tonto-finishing-model
description: Finishing the University model
sidebar_position: 6
---

# Finishing Model

The last step is to get our final model relating the PersonPhases package and the University package. Take a look at the
diagram for this final model:

![Example model in OntoUML of an University](/img/diagrams/fig-diagrams-university-model.png)

The main difference is that we have two new elements, the relators *Employment Contract* and *Enrollment*. We could add it to
any package, and in our case we will add it to the existing University package. Add the following relators to your code:

```text
relator EmploymentContract {
  @mediation
  [1..*] -- [1] Employee
  @mediation
  [1..*] -- [1] Employer
}

relator Enrollment {
    @mediation
    [0..*] -- [1] University

    @mediation
    [1..*] -- [1] UniversityStudent
}
```

## Finished packages

The finished package files can be checked here:

### PersonPhases.tonto

```text
import CoreDatatypes

package PersonPhases

kind Person

type PersonTypeByAge

phase Child
phase Teenager
phase Adult

disjoint complete genset PhasesOfPerson {
  general Person
  specifics Child, Teenager, Adult
}

role UniversityStudent specializes Person
role FormerStudent specializes UniversityStudent
role ActiveStudent specializes UniversityStudent

role Employee specializes Person
role UniversityProfessor specializes Employee
```

### CoreDatatypes.tonto

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

datatype Address {
  country: string
  city: string
  postalCode: string
  street: string
  number: string
  complement: string
}
```

### University.tonto

```text
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

relator EmploymentContract {
  @mediation
  [1..*] -- [1] Employee
  @mediation
  [1..*] -- [1] Employer
}

relator Enrollment {
  @mediation
  [0..*] -- [1] University

  @mediation
  [1..*] -- [1] UniversityStudent
}
```
