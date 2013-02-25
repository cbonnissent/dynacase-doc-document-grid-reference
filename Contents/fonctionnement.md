# Fonctionnement {#document-grid-ref:ad9f0c7e-64a6-4f1e-9e6c-4297e78f0f41}

La documentGrid fonctionne en lien avec le serveur Dynacase, le principe de fonctionnement est le suivant :

1.  Déclaration de la documentGrid côté client,
2.  Si nécessaire (présence de colonnes liées à  des attributs ou des propriétés),
    la documentGrid fait un appel serveur pour récupérer l'intégralité de la définition des colonnes
    (colonne triable, filtrable, label de la colonne, type de la colonne),
3.  La documentGrid utilise la définition des colonnes pour construire un objet de configuration adapté à la dataGrid (objet aoColumsDef),
4.  Si la documentGrid est filtrable alors elle construit le footer de la balise table en y ajoutant les filtres nécessaires suivant les colonnes filtrables,
5.  La documentGrid initie la dataTable,
6.  La dataTable effectue le premier chargement de ses données,
7.  La dataTable effectue le rendu des lignes en fonction des données reçues,
8.  Si la documentGrid doit initier le système d'overlay, elle l'attache à la dataTable nouvellement générée,
9.  À chaque opération effectuée sur la table (changement de page, filtre, tri),
    la dataTable va chercher sur le serveur les données nécessaire à son rafraîchissement et se reconstruit.
