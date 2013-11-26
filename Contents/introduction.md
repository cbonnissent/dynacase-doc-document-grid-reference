# Introduction {#document-grid-ref:8bb07809-1742-4938-994f-604159da62ed}

## Fonctionnalités {#document-grid-ref:378ecbb9-5e22-4343-98c9-602c14618e9e}

Document Grid  est un plugin Dynacase permettant de construire une interface de
consultation de documents sous la forme d'une table HTML dynamique. Ce plugin
est bas niveau et est destiné à être intégré dans une page web.

## Paradigme {#document-grid-ref:3c8d5f85-2274-40df-a0f9-062173699156}

La documentGrid est construite sur le pattern [widget][jquery-ui-widget] de
[jquery-ui][jquery-ui] et se comporte donc comme un widget jquery-ui
(initialisation, options, évènements, etc.) et est basée sur le plugin
[datatable][jquery-datatables] de jQuery.

Lors de la création d'une documentGrid le plugin génère un objet d'options
approprié pour une dataTable et injecte ensuite cette dataTable dans la page
courante.

[jquery-ui]: http://jqueryui.com/
[jquery-ui-widget]: http://jqueryui.com/widget/
[jquery-datatables]: http://www.datatables.net/