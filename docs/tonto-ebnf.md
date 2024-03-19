---
id: tonto-ebnf
sidebar_position: 7
---

# Tonto EBNF Declaration

In this page, we delineate the Extended Backus-Naur Form (EBNF) declaration pertinent to Tonto. The PDF version can be found [here.](https://matheuslenke.github.io/tonto-docs/pdf/Tonto-EBNF.pdf) 

```bnf
grammar Tonto

entry Model:
	imports+=Import*
	packageDeclaration=PackageDeclaration
;

/**
 * Package declaration
 */

PackageDeclaration:
	(isGlobal?='global')? 'package' (name=QualifiedName | name=STRING)

	declarations+=Declaration*
;

Import:
	'import' referencedModel=[PackageDeclaration:QualifiedName] ('as' packageAlias=ID)?
;

// <--- Declarations --->

Declaration:
	ClassDeclarationRule | AuxiliaryDeclaration
;

AuxiliaryDeclaration:
	DataType | Enum | GeneralizationSetImpl | GeneralizationSetShort | ExternalRelation
;

/**
* Class Declaration
*/

ClassDeclarationRule returns ClassDeclaration:
	classElementType=OntologicalCategory 
	name=QualifiedName
	ontologicalNatures=ElementOntologicalNature?
    ('(' 'instanceOf' instanceOf=[ClassDeclaration:QualifiedName] ')')?
    ('specializes' specializationEndurants+=[ClassDeclaration:QualifiedName]
		(',' specializationEndurants+=[ClassDeclaration:QualifiedName])?
		)? 
		('{'
			(attributes+=Attribute | references+=InternalRelation)*
    '}')?
;

type DataTypeOrClass = DataType | ClassDeclaration;
type DataTypeOrClassOrRelation = DataType | ClassDeclaration | ElementRelation;

/**
* Ontological Category
*/

OntologicalCategory:
	ontologicalCategory=(UnspecifiedType | NonEndurantType | EndurantType)
;

UnspecifiedType returns string:
	'class'
;

NonEndurantType returns string:
	'event' | 'situation' | 'process'
;

EndurantType returns string:
	NonSortal | UltimateSortal | Sortal;


NonSortal returns string:
	'category' | 'mixin' | 'phaseMixin' | 'roleMixin' | 'historicalRoleMixin'
;

UltimateSortal returns string:
	'kind' | 'collective' | 'quantity' | 'quality' | 'mode' | 'intrinsicMode' | 'extrinsicMode' | 'relator' | 'type' | 'powertype'
;

Sortal returns string:
	'subkind' | 'phase' | 'role' | 'historicalRole'
	
/**
* Ontological Nature
*/

ElementOntologicalNature:
	'of' natures+=OntologicalNature (',' natures+=OntologicalNature)*
;

OntologicalNature returns string:
	'objects' | 'functional-complexes' | 'collectives'  | 'quantities' |
    'relators' | 'intrinsic-modes' | 'extrinsic-modes' | 'qualities' |
    'events' | 'situations' |  'types' | 'abstract-individuals'
;

/**
* Attributes
*/

Attribute:
	name=ID ':' attributeTypeRef=[DataType:QualifiedName]
	cardinality=Cardinality?
	('{'((isOrdered?='ordered') & (isConst?='const') & (isDerived?='derived'))? '}')?
;

Cardinality:
	'[' lowerBound=(INT | '*')
	('..' upperBound=(INT | '*'))? ']'
;

/**
* Relations
*/

ElementRelation:
	InternalRelation | ExternalRelation
;

InternalRelation infers ElementRelation:
	('@'relationType=RelationStereotype)?
	RelationData
;

ExternalRelation infers ElementRelation:
	('@'relationType=RelationStereotype)?
	'relation' firstEnd=[ClassDeclaration:QualifiedName]
	RelationData
;

fragment RelationData:
	firstEndMetaAttributes=RelationMetaAttributes?
	firstCardinality=Cardinality?
	RelationName
	secondCardinality=Cardinality?
	secondEnd=[DataTypeOrClassOrRelation:ID]
	
	secondEndMetaAttributes=RelationMetaAttributes?
	('specializes' specializeRelation=[ElementRelation:QualifiedName])?
	(hasInverse='inverseOf' inverseEnd=[ElementRelation:QualifiedName])?
;

fragment RelationName:
	(RelationType ((name=QualifiedName | name=STRING) '--')?) |
	(('--' name=QualifiedName | name=STRING)? RelationInvertedType)?
;

fragment RelationType:
 (isAssociation?='--' | isAggregation?='<>--' | isComposition?='<o>--')
;

fragment RelationInvertedType:
	isAggregationInverted?='--<>' | isCompositionInverted?='--<o>'
;

RelationMetaAttributes:
	'('
	('{' endMetaAttributes+=RelationMetaAttribute
	(',' endMetaAttributes+=RelationMetaAttribute )* '}')?
	(endName=ID)?
	')'
;

RelationMetaAttribute:
	isOrdered?='ordered' | isConst?='const' | isDerived?='derived' |
	('subsets' subsetRelation=[ElementRelation:QualifiedName] ) |
	('redefines' redefinesRelation=[ElementRelation:QualifiedName] )
;

RelationStereotype returns string:
	'material' |
	'derivation' |
	'comparative' |
	'mediation' |
	'characterization' |
	'externalDependence' |
	'componentOf' |
	'memberOf' |
	'subCollectionOf' |
	'subQuantityOf' |
	'instantiation' |
	'termination' |
	'participational' |
	'participation' |
	'historicalDependence' |
	'creation' |
	'manifestation' |
	'bringsAbout' |
	'triggers' |
	'composition' |
	'aggregation' |
	'inherence' |
	'value' |
	'formal' |
	'manifestation' |
	'constitution' |
	ID |
	STRING
;

/**
* GenSets
*/

type ClassDeclarationOrRelation = ClassDeclaration | ElementRelation;

GeneralizationSet:
	(disjoint?='disjoint')? (complete?='complete')?
	'genset' name=ID '{'
			(
				'general' generalItem=[ClassDeclarationOrRelation:QualifiedName]
				('categorizer' categorizerItems+=[ClassDeclarationOrRelation:QualifiedName])?
				'specifics' specificItems+=[ClassDeclarationOrRelation:QualifiedName]
				(',' specificItems+=[ClassDeclarationOrRelation:QualifiedName])*
			)
	'}'
;

GeneralizationSetShort returns GeneralizationSet:
	(disjoint?='disjoint')? (complete?='complete')?
	'genset' name=ID 'where' 
	specificItems+=[ClassDeclarationOrRelation:QualifiedName] 	(',' specificItems+=[ClassDeclarationOrRelation:QualifiedName])*
	'specializes' generalItem=[ClassDeclarationOrRelation:QualifiedName]
;

/**
* DataTypes
*/

DataType:
	'datatype' name=ID ontologicalNature=ElementOntologicalNature? 
	('specializes' specializationEndurants+=[DataTypeOrClass:QualifiedName]
	(',' specializationEndurants+=[DataTypeOrClass:QualifiedName])?
	)? 
	('{'
		(attributes+=Attribute)*
	'}')?
;

Enum infers DataType:
	isEnum?='enum' name=ID 
	('specializes' specializationEndurants+=[DataTypeOrClass:QualifiedName]
	(',' specializationEndurants+=[DataTypeOrClass:QualifiedName])?
	)? 
	'{'
		(elements+=EnumElement
		((',') elements+=EnumElement)*)?
	'}'
;

EnumElement:
	name=ID
;

/**
* Terminals
*/

hidden terminal WS: /\s+/;
terminal ID: /[_a-zA-Z][\w_]*/;
terminal INT returns number: /[0-9]+/;
terminal STRING: /"[^"]*"|'[^']*'/;

hidden terminal ML_COMMENT: /\/\*[\s\S]*?\*\//;
hidden terminal SL_COMMENT: /\/\/[^\n\r]*/;

QualifiedName returns string:
	ID ('.' ID)*
;
```