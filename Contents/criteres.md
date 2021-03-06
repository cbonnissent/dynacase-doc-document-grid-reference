# Critères

La table peut aussi accepter en entrées un ensemble de critères, ceux-ci sont appliqués à la collection associées à la table (ou le searchDoc le cas échéant) et seuls les éléments satisfaisant à ces critères sont présentés dans la table et apparaissent dans les décomptes.

Les critères se présentent sous la forme d'un array javascript dont chaque ligne est un objet avec le formalisme suivant :

* *id* : attribut ou propriété sur lequel la collection est filtrée (seules les propriété state et title sont utilisables, les attributs de type time et color ne sont pas pris en compte) (chaîne de caractères),
* *type* : type de l'attribut/propriété en cours (la propriété title doit avoir un type text) (chaîne de caractères),
* *multiplicity* : multiplicité de l'attribut/propriété en cours. Deux valeurs sont possibles : "simple", "multiple". (Les propriétés doivent être de multiplicité "simple") (chaîne de caractère),
* *value* : valeur du critère de recherche. La valeur peut être sous différents formats suivant le type, la multiplicité et l'opérateur.
	*objet javascript* : objet js contenant deux clefs valueMin et valueMax contenant chacune une chaîne de caractères pour les critères ayant un opérateur between,
	*tableau javascript* : chaque item est soit un id, soit une clef pour les attributs de type enum, docid multiples, 
	*chaîne de caractère* : pour tous les autres types d'attributs et d'opérateurs qui ne sont pas mentionnés ci-dessus
* *opérateur* : l'opérateur est une chaîne de caractères décrivant le type de recherche qui sera appliqué, la liste est la suivante :

	* *dc:na* : applicable à tous les types d'attributs/propriété indique que le critère ne sera pas pris en compte,
	* *dc:empty* : applicable à tous les types d'attributs/propriété indique que seuls les élements vide seront retenu. SQL suivant la multiplicité :

		* *simple* : %1$s is NULL,
		* *multiple* : replace(%1$s, '<BR\>', E'\\n') ~ E'^\\\\n+$' or %1$s is NULL'
	* *dc:not empty* : applicable à tous les types d'attributs/propriété indique que seuls les élements vide seront retenu. SQL suivant la multiplicité :

		* *simple* : %1$s is not NULL,
		* *multiple* : replace(%1$s, '<BR\>', E'\\n') !~ E'^\\\\n+$'

	* *dc:equal* : applicable aux types : "int", "double", "money", "date", "timestamp", "state", "enum", "docid", "account".SQL suivant la multiplicité :

		* *simple* : %1$s = '%2$s',
        * *multiple* : replace(%1$s, '<BR\>', E'\\n') = '%2$s'

	* *dc:not equal* : applicable aux types : "int", "double", "money", "date", "timestamp", "state", "enum", "docid", "account".SQL suivant la multiplicité :

		* *simple* : %1$s <> '%2$s' or %1$s is NULL',
        * *multiple* : replace(%1$s, '<BR\>', E'\\n') <> '%2$s' or %1$s is NULL

	* *dc:inferior* : applicable aux types : "int", "double", "money", "date", "timestamp".SQL suivant la multiplicité :

		* *simple* : %1$s < '%2$s'

	* *dc:superior* : applicable aux types : "int", "double", "money", "date", "timestamp".SQL suivant la multiplicité :

		* *simple* : %1$s > '%2$s'

	* *dc:between* : applicable aux types : "int", "double", "money", "date", "timestamp".SQL suivant la multiplicité :

		* *simple* : %1$s >= '%2$s' and %1$s <= '%3$s'

	* *dc:contain* : applicable aux types : "text", "htmltext", "longtext".SQL suivant la multiplicité :

		* *simple* : %1$s ~* '%2$s'

	* *dc:not contain* : applicable aux types : "text", "htmltext", "longtext".SQL suivant la multiplicité :

		* *simple* : %1$s !~* '%2$s' or %1$s is NULL

	* *dc:one contain* : applicable aux types : "text", "htmltext", "longtext".SQL suivant la multiplicité :

		* *multiple* : %1$s ~* '%2$s'

	* *dc:no one contain* : applicable aux types : "text", "htmltext", "longtext".SQL suivant la multiplicité :

		* *multiple* : %1$s !~* '%2$s' or %1$s is NULL

	* *dc:one equal* : applicable aux types : "int", "double", "money", "date", "timestamp".SQL suivant la multiplicité :

		* *multiple* : '%2$s' = ANY (regexp_split_to_array(replace(%1$s, '<BR\>', E'\\n'), E'\\n' ))

	* *dc:no one equal* : applicable aux types : "int", "double", "money", "date", "timestamp".SQL suivant la multiplicité :

		* *multiple* : '%2$s' <> ALL (regexp_split_to_array(replace(%1$s, '<BR\>', E'\\n'), E'\\n' )) or %1$s is NULL

	* *dc:with* : applicable aux types : "state", "enum", "docid", "account".SQL suivant la multiplicité :

		* *multiple* : ARRAY[%2$s] && (regexp_split_to_array(replace(%1$s, '<BR\>', E'\\n'), E'\\n' ))

	* *dc:without* : applicable aux types : "state", "enum", "docid", "account".SQL suivant la multiplicité :

		* *multiple* : not(ARRAY[%2$s] && (regexp_split_to_array(replace(%1$s, '<BR\>', E'\\n'), E'\\n' ))) or %1$s is NULL

*note* : dans la documentation %1$s correspond à l'id en cours et %2$s, %3$s aux valeurs en cours.
*note* : les opérateurs n'ayant de SQL pour un type de multiplicité ne sont applicables à celui-ci.

