---
id: tonto-relations
description: Test
sidebar_position: 4
---

# Adding relations to your Model

Relations (or UML associations) are an important part of conceptual modeling in OntoUML, providing meaning to the
connections between elements. They are also a core concept in Tonto and can be declared in two different ways. The first
way is called an internal relation, which is defined inside the body of the declaration of a class. The second way is
called an external relation and can be defined outside the body of class declarations.

We use the OntoUML model in the figure above to discuss relations in the sequel. This model presents University as a
<Stereotype>kind</Stereotype> that specializes the category *Organization* of functional complexes. The university
possibly has many *Classrooms*, and that is stated with the aggregation relation between them named "has". Because the
classroom is a specific kind of room, it specializes the kind *Room*. Also, the university has one or more *Departments*,
and this is expressed with an aggregation relation with the stereotype <Stereotype>componentOf</Stereotype>. The
department is composed by a *JuniorStaff* and a *SeniorStaff*, also represented with an aggregation relation. These
staffs are subkind of the collective *Staff*. Moreover, we have a roleMixin *Employer*, that aggregates properties in
common to everything that hires someone. The role *UniversityEmployer* represents the capacity that this university have
to hire employees, for example for its junior and senior staff.

![Relations example diagram](/img/diagrams/fig-diagrams-example2.png)

From this diagram we can represent in Tonto the kind *University* with its relations with the following code:

```text
kind University specializes Organization {
  address: Address
  @componentOf
  [1] <>-- has -- [1..*] Department 
  @componentOf
  [1] <>-- [0..*] Classroom 
}
```

First, on lines 3 and 4 we have a relation named *has* with the stereotype <Stereotype>componentOf</Stereotype>, stated
with a keyword prefixed with the ``@`` symbol (a syntax inspired in Java annotations). Every OntoUML relation stereotype
can be declared that way. Being an internal relation, the element of the first end is the class holding the relation and
its name is omitted. Relation specification works like a mirror (inspired in the UML notation for association, which is
a line with opposing association ends), where the definition order for the element in the first end is inverted for the
second end. The order of declaration in the first relation end is, after the relation stereotype: class ID (in case of
an external relation); first end meta-attributes; first end name; first end cardinality and the relation connector with
its name. Meta-properties of a relation can be ``ordered``, ``const`` and ``derived``.

Moreover, the first cardinality represents the cardinality on the University end, and the second cardinality of [1]
represents the Department end of the relation. The default cardinality of relations is one to one, and can be omitted in
that case.  Because it is an aggregation relation, the keyword ``'<>- -'`` is used. For associations, the keyword is
``'- -'``, and for composition is ``'<o>- -'``. These keywords defines the `middle' point of an relation, where the
relation name can be defined after this connector keyword, and an extra keyword ``'- -'`` is added after its name.

After the second end class ID, two other properties can be defined: a specialization of the relation and the inverse of
this relation. Specialization uses the same ``specializes`` keyword used in classes, and inverses use the ``inverseOf``
keyword, both of them followed by the relation ID.

Further, we can express the relation between *JuniorStaff* and *SeniorStaff* externally. The code below shows the
definition of these two external relations. The only difference between them is the need for the keyword *relation* and
the name of the first end class; every other component of the relation is declared in the same way as an internal
relation and in the same order.

```text
relation Department [1] <>-- [1] JuniorStaff
relation Department [1] <>-- [1] SeniorStaff
```

export const Stereotype = ({children}) => (
  <i
  >
  ≪{children}≫
  </i>
);
