# Test

Le plugin documentGrid est fourni avec une application permettant de la tester sans faire l'ensemble de l'intégration.

Cette application est accessible aux utilisateurs ayant le droit TEST de l'application DOCUMENT_GRID_TEST à l'adresse suivante : 

&lt;url_de_base&gt;?app=DOCUMENT_GRID_TEST

Elle permet de piloter la documentGrid en bas de la page à l'aide de la zone de saisie "objet de configuration". De plus, il est possible de sauvegarder un objet de configuration en cliquant sur le bouton "save", celui sera alors sauvé dans le localstorage de la page en cours et peut être retrouvé à l'aide du menu déroulant sélectionner un exemple.

De plus, en bas de la page est présenté une balise &lt;pre&gt; qui contient le compte rendu des erreurs relevées par la table lors de son fonctionnement.

*note:* l'objet de configuration fourni par défaut est un exemple et ne fonctionne pas sur une installation basique, il vous faut définir votre collection et choisir une famille par défaut existant sur votre contexte.
