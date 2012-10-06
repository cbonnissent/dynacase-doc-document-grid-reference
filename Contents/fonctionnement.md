# Fonctionnement

La documentGrid fonctionne en lien avec le serveur Dynacase, le principe de fonctionnement est le suivant :

* Déclaration de la documentGrid côté client,
* Si nécessaire (présence de colonnes liées à  des attributs ou des propriétés) la documentGrid fait un appel serveur pour récupérer l'intégralité de la définition des colonnes (colonne triable, filtrable, label de la colonne, type de la colonne),
* La documentGrid utilise la définition des colonnes pour construire un objet de configuration adapté à la dataGrid (objet aoColumsDef),
* Si la documentGrid est filtrable alors elle construit le footer de la balise table en y ajoutant les filtres nécessaires suivant les colonnes filtrables,
* La documentGrid initie la dataTable,
* La dataTable effectue le premier chargement de ses données,
* La dataTable effectue le rendu des lignes en fonction des données reçues,
* Si la documentGrid doit initier le système d'overlay, elle l'attache à la dataTable nouvellement générée,
* A chaque opération effectuée sur la table (changement de page, filtre, tri) la dataTable va chercher sur le serveur les données nécessaire à son rafraîchissement et se reconstruit.
