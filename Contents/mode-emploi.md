# Mode d'emploi {#document-grid-ref:47c10fee-7d50-4a0d-acd9-9fd9e1d1c658}

## Dépendances {#document-grid-ref:b77dc4cd-c01b-459e-bb0a-2b0cb397bcf1}

L'intégration du plugin requiert l'ajout dans la page web des composants suivants :

* **json2** : `lib/data/json2.js`  
    cet élément est nécessaire pour faire fonctionner le plugin sur les navigateurs ne possédant pas l'objet `JSON`.
* **jquery** : `lib/jquery/jquery.js`
* **jquery-ui** : `lib/jquery-ui/js/jquery-ui-1.8.21.custom.min.js` & `lib/jquery-ui/css/smoothness/jquery-ui-1.8.21.custom.css`
* **jquery dataTables** : `lib/jquery-dataTables/js/jquery.dataTables.min.js` & `lib/jquery-dataTables/css/jquery.dataTables_themeroller.css`
* **jquery docGrid** : `DOCUMENT_GRID_UI/Layout/jquery.docGrid-code.js` & `DOCUMENT_GRID_UI/Layout/jquery.docGrid.css`

Les adresses des éléments sont données à titre indicatif et sont valables dans
l'optique d'une intégration au sein d'une application/action.

## Droits {#document-grid-ref:ab08967e-c25e-4fd7-8997-3e6a2f71a20d}

Les utilisateurs devant avoir accès à DocumentGrid et ses actions associées
doivent avoir l'ACL : *BASIC* de l'application *DOCUMENT_GRID_UI*.

## Initialisation {#document-grid-ref:be129832-025e-4939-9bb2-09c5b4271077}

Idéalement l'initialisation du plugin doit avoir lieu sur l'évènement *ready* de
la page en cours pour permettre à la DOM et aux dépendances d'être chargées au
préalable.

L'initialisation de la documentGrid se fait sur une balise `<table>`, celle-ci
doit être pré-existante à l'initialisation. On doit ensuite la sélectionner à
l'aide de jQuery et l'initialiser.


Exemple d'initialisation de documentGrid contenant le titre et un bouton
permettant d'ouvrir le document :

    [html]
    <html>
        <head>
            <title>DocumentGrid</title>
            
            <link href="lib/jquery-ui/css/smoothness/jquery-ui.css" rel="stylesheet" type="text/css"/>
            <link href="lib/jquery-dataTables/css/jquery.dataTables_themeroller.css" rel="stylesheet" type="text/css" />
            <link href="DOCUMENT_GRID_UI/Layout/jquery.docGrid.css" rel="stylesheet" type="text/css" />
            
            <script type="text/javascript" src="lib/jquery/jquery.js"></script>
            <script type="text/javascript" src="lib/jquery-ui/js/jquery-ui.js"></script>
            <script type="text/javascript" src="lib/jquery-dataTables/js/jquery.dataTables.min.js"></script>
            <script type="text/javascript" src="DOCUMENT_GRID_UI/Layout/jquery.docGrid-code.js"></script>
            
            <script type="text/javascript">
                $(document).on("ready", function () {
                    $("#mydocGrid").docGrid({
                        collection : "MY_COLLECTION",
                        columnsDef : {
                            "defaultFam" : "MYDEFAULTFAM",
                            "columns" : [
                                {type : "openDoc"},
                                {id : "title"}
                            ]
                        }
                    });
                });
            </script>
        </head>
        
        <body>
            <table id="mydocGrid"></table>
        </body>
        
    </html>

### Options de configuration {#document-grid-ref:405a40cd-9f17-42c8-b08e-ce79f06c13f0}

Les éléments en gras sont obligatoires.

**collection**
:   nom logique d'une collection, elle est la source des données affichées,  
    *type* : chaîne de caractères ;

**columnsDef**
:   configuration des colonnes (voir le détail dans le [paragraphe dédié][columnsDef]),  
    *type* : objet javascript 

filterable
:   indique si grille proposera ou pas des filtres  
    *type* :booléen,  
    *valeur par défaut* : `false` ;

sortable
:   indique si la grille proposera ou pas la possibilité de trier les éléments par colonnes  
    *type* :booléen,  
    *valeur par défaut* : `true` ;

dataTableOptions 
:   objet de configuration de la dataTable associée à la documentGrid,  
    **Note** : Les options passées par cette entrée ne sont supportées via le contrat de support,
    il appartient au développeur de tester le comportement et de faire ci-besoin 
    les ajustements nécessaires.  
    *type* : objet javascript  ;

withOverlay
:   indique si le système d'overlay doit être chargé avec la grille, ce système permet d'ouvrir les liens générés par la grille dans une fenêtre modale.  
    *type* :booléen,  
    *valeur par défaut* : `true` ;

offlineColumnsDef 
:   active ou désactive la recherche de la définition des colonnes sur le serveur.
    Passer ce paramètre à false évite une requête au serveur lors de l'initialisation du widget, mais vous devez alors fournir la définition complète.  
    *type* :booléen,  
    *valeur par défaut* : `false` ;

autoload
:   active ou désactive le chargement de la table lors de l'initialisation.
    Lorsque ce paramètre est à false, la table est chargée sans requête server et sans données.
    l'IHM indique alors "aucune données" et "résultats 0 sur 0".
    À charge du progammeur de customizer l'IHM.  
    *type* :booléen,  
    *valeur par défaut* : `true` ;

gridDataSourceUrl
:   url de récupération des données alimentant la base  
    *type* : chaîne de caractères,  
    *valeur par défaut* : `"?app=DOCUMENT_GRID_UI&action=GETJSONDOCGRIDCONTENT"` ;

columnsDefUrl
:   url de récupération de la définition des colonnes de la tables, inutile si offlineColumnsDef est à `false`  
    *type* : chaîne de caractères,  
    valeur par défaut : `"?app=DOCUMENT_GRID_UI&action=GETCOLUMNSDEFINITION"` ;

filterEnumContentUrl
:   url de récupération des listes déroulantes pour les énumérés  
    *type* : chaîne de caractères,  
    valeur par défaut : `"?app=DOCUMENT_GRID_UI&action=GETENUMCONTENT"` ;

filterStateContentUrl
:   url de récupération des listes déroulantes pour les états  
    *type* : chaîne de caractères,  
    valeur par défaut : `"?app=DOCUMENT_GRID_UI&action=GETSTATES"` ;

criterias
:   tableau de configuration de critères s'appliquant à la table. Le format des critères est décrit dans le [chapitre sur les critères][criteres].

Pour mettre à jour une option après l'initialisation, on utilise la syntaxe suivante :

    [javascript]
    $("#mydocGrid").docGrid("option", "<option_name>", "<value>");

*note* : seules les options *collection* et *criterias* peuvent changées une fois la grille initialisée.

#### columnsDef {#document-grid-ref:e1408dca-0c10-4c33-bb1c-8aeab1f69ef1}

Cet objet de configuration donne les éléments permettant d'établir la
configuration des colonnes de la dataTable. Pour ce faire, il possède les
propriétés `defaultFam` et `columns`.

defaultFam
:   nom logique de la famille par défaut des attributs des colonnes  
    *type* : chaîne de caractères

**columns**
:   Tableau de définition des colonnes.
    Chaque élément est un objet composé des éléments suivants :
    
    id
    :   nom logique de l'attribut/propriété contenu dans cette colonne  
        *type* : chaîne de caractères
    
    label
    :   nom de la colonne à afficher  
        *type* : chaîne de caractères
    
    famId
    :   famille contenant l'attribut id  
        *type* : chaîne de caractères.  
        Cet élément n'est pas obligatoire dans les cas suivants :
        
        * defaultFam est défini,
        * l'élément à représenter est une propriété,
        * l'élément à représenter est une colonne virtuelle.
    
    sortable
    :   indique si la colonne est triable.  
        Cette valeur est calculée automatiquement si l'élément en cours est une propriété ou un attribut, sinon sa valeur par défaut est false  
        *type* : booléen
    
    filterable
    :   indique si la colonne est filtrable  
        Cette valeur est calculée automatiquement si l'élément en cours est une propriété ou un attribut, sinon sa valeur par défaut est false  
        *type* : booléen
    
    type
    :   indique le type de la colonne.  
        Il est utilisé pour définir le type de rendu de la colonne ou pour définir des colonnes virtuelles.
        Dans ce cas, il faut utiliser le type `"void"`  
        Cette valeur est calculée automatiquement si l'élément en cours est une propriété ou un attribut, sinon sa valeur est obligatoire.  
        *type* : chaîne de caractères.  
        Les types *virtuels* pré-définis sont :
        
        openTitle
        :   ajoute une colonne permettant d'ouvrir le document en cours avec le titre du document comme lien,
        
        openDoc
        :   ajoute une colonne avec un bouton pour ouvrir le document.
            Ouvre le document dans un overlay si *withOverlay* est à true
    
    render
    :   Permet de surcharger le rendu spécifique d'une colonne.  
        Un render par défaut est fourni sur l'ensemble des colonnes de type attribut/propriété.
        Il est appelé avec la string "text", et permet d'avoir un rendu textuel de la colonne.  
        Sinon render doit être une fonction qui retourne une chaine de caractère qui sera parsée en DOM
        et intégrée dans la cellule en cours de la table.
        Elle reçoit en entrée la ligne en cours et a pour scope l'objet de configuration de la colonne en cours
        *type* : fonction ou string
    
    withIcon
    :   indique si une icône doit accompagner le rendu de la colonne en cours.  
        *type* : booléen  
        Cette option est valide pour les colonnes de type :
        
        *   title,
        *   openDoc,
        *   openTitle,
        *   docid,
        *   file,
        *   image
    
    withColor
    :   indique si la couleur doit accompagner le rendu de l'état.
        Cette option est valide pour les colonnes de type state  
        *type* : booléen,  
        *valeur par défaut* : `false`
    
    docTitle
    :   indique le nom de l'attribut docTitle.
        Cette option est valide pour les colonnes de type relation sur lesquel un filtre est prévu.
        Elle est calculée automatiquement si la grille n'est pas en mode offlineColumnsDef.  
        *type* : chaîne de caractères

Lors de la définition d'une colonne doivent être présent a minima soit l'id,
soit le type.

**Note** : Vous pouvez utiliser [d'autres options][jquery-datatables-columns-options] 
propres aux colonnes de la datatable mais dans ce cas le fonctionnement n'est pas
garanti et il appartient au développeur de faire les ajustements nécessaires.

## Méthodes associées {#document-grid-ref:d1c034a3-eb0b-4cc4-89b1-7892642b1428}

Plusieurs méthodes sont associées à l'objet documentGrid :

destroy
:   Permet de détruire la table.  
    La table ne peut pas être détruite avant son initialisation, toutefois dans 
    ce cas l'ordre de destruction est enregistré et appliqué à la fin du chargement.
    La table est alors supprimée (la balise reste en place, mais son contenu est vidé),

refresh
:   Permet de rafraîchir la table.
    Celle-ci conserve son état courant (page en cours, tri, filtre), mais recharge ses données en effectuant une requête serveur.

getFilters
:   Permet de récupérer les filtres actuellement en cours sur la grille, sous la
    forme d'un tableau d'objets JavaScript.

setFilters
:   Permet de définir les filtres actuellement en cours sur la grille. Cette 
    fonction prend comme argument un array contenant des objets de la forme 
    suivantes :
    
    * **id** : identifiant du filtre (attrid de l'attribut correspondant
     à la colonne),
    * **value** : valeur,
    * **text** : texte à afficher valable pour les filtres d'attributs `enum`
     et `state`.

resetFilters
:   Remet les filtres à leur valeur initiale. C'est à dire sans valeur.

Ces méthodes sont appelées avec la syntaxe suivante :

    [javascript]
    $("#mydocGrid").docGrid("<fonction_name>");

## Événement associés {#document-grid-ref:3d241ffa-9893-4f07-a0c8-7fe44659013c}

error
:   déclenché à chaque erreur détectée par la dataTable.  
    Il fournit un objet event et un objet erreur (tableau de messages d'erreurs),

change
:   déclenché à chaque rechargement de la table (filtrage, changement de page, etc).
    Il fournit un objet event et un objet contenant les informations qui vont être transmises à la dataTable.
    La modification de cet objet est déconseillée car elle peut avoir comme effet de bord de modifier le contenu de la table.

redraw
:   déclenché après la mise à jour de la table et son ajout dans la page web.

Les évènements peuvent être écoutés de deux manières différentes :

*   En utilisant les fonctionnalités pour s'attacher à un évènement de jQuery.  
    Il faut alors préfixer l'évènement cible par le nom du widget en minuscule (dans notre cas *docgrid*)

    [javascript]
    $("#mydocGrid").on("docgriderror", function(e, ui) { console.log(ui);});

*   En s'inscrivant directement à la création du widget :

    [javascript]
    $("#mydocGrid").docGrid({ error : function(e, ui) { console.log(ui);}};

[criteres]:                             #document-grid-ref:57ef9e48-731e-46ff-aa8e-ce5c015a3b42
[columnsDef]:                           #document-grid-ref:e1408dca-0c10-4c33-bb1c-8aeab1f69ef1
[jquery-datatables-options]:            http://www.datatables.net/usage/options
[jquery-datatables-columns-options]:    http://datatables.net/usage/columns