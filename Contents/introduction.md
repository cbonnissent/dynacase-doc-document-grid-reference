# Introduction

## Fonctionnalités

Document Grid  est un plugin Dynacase permettant de construire une interface de consultation de documents sous la forme d'une table HTML dynamique. Ce plugin est bas niveau et est destiné à être intégré dans une page web.

## Paradigme

La documentGrid est construite sur le pattern [widget][jquery-ui-widget] de [jquery-ui][jquery-ui] et se comporte donc comme un widget jquery-ui (initialisation, options, évènements, etc.) et est basée sur le plugin [datatable][jquery-datatables] de jQuery.

Lors de la création d'une documentGrid le plugin génère un objet d'options approprié pour une dataTable et injecte ensuite cette dataTable dans la page courante.

[jquery-ui]: http://jqueryui.com/
[jquery-ui-widget]: http://jqueryui.com/widget/
[jquery-datatables]: http://www.datatables.net/