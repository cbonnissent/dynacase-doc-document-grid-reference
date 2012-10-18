# Backend PHP

Les parties cliente et serveur communiquent via des requêtes *ajax*, et le contenu est formaté en JSON.

Le backend par défaut est défini dans le fichier `DOCUMENT_GRID_UI/getdocgridcontent.php` et est porté par la fonction `getdocgridcontent`, dont le résultat est ensuite encodé en JSON.

Il est possible de créer un backend PHP spécialisé en se basant sur celui par défaut. Pour ce faire le plus simple, et d'intégrer le backend par défaut dans le nouveau.

Un des backend les plus simple que l'on peut créer est celui par défaut qui se présente de la manière suivante :

    [php]
    <?php

    require_once 'DOCUMENT_GRID_UI/getdocgridcontent.php';

    function getjsondocgridcontent(Action &$action)
    {
        $content = getdocgridcontent($action);
        $action->lay->template = json_encode($content);
        $action->lay->noparse = true;

        header('Content-type: application/json');
    }

    ?>

Il intègre le backend par défaut en faisant un require du fichier PHP et ensuite appelle la méthode getdocgridcontent en renvoyant son retour en json.

Il est à noter que getdocgridcontent peut prendre en deuxième paramètre un objet SearchDoc et que dans ce cas il n'utilise pas de collection.

Pour pouvoir utiliser un nouveau backend, il faut le déclarer lors de l'initialisation de la docGrid de la manière suivante :

    [html]
    <html>
        <head>
            <title>DocGrid</title>

            <link href="lib/jquery-ui/css/smoothness/jquery-ui-1.8.21.custom.css" rel="stylesheet" type="text/css" />
            <link href="lib/jquery-dataTables/css/jquery.dataTables_themeroller.css" rel="stylesheet" type="text/css" />
            <link href="DOCUMENT_GRID_UI/Layout/jquery.docGrid.css" rel="stylesheet" type="text/css" />

            <script type="text/javascript" src="lib/jquery/jquery.js"></script>
            <script type="text/javascript" src="lib/jquery-ui/js/jquery-ui-1.8.21.custom.min.js"></script>
            <script type="text/javascript" src="lib/jquery-dataTables/js/jquery.dataTables.min.js"></script>
            <script type="text/javascript" src="DOCUMENT_GRID_UI/Layout/jquery.docGrid.js"></script>

            <script type="text/javascript">
                $(document).on("ready", function () {
                    $("#mydocGrid").docGrid({
                        columnsDef : {
                            "defaultFam" : "MYDEFAULTFAM",
                            "columns" : [
                                {type : "openDoc"},
                                {id : "title"}
                            ]
                        }
                        dataTableOptions: {
                            sAjaxSource: "?app=MYAPP&action=MYBACKEND"
                        }
                    });
                });
            </script>
        </head>

        <body>
            <table id="mydocGrid"></table>
        </body>

    </html>

