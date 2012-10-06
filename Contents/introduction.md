# Introduction

## Fonctionnalités

Document Grid  est un plugin Dynacase permettant de construire une interface de consultation de documents sous la forme d'une table HTML dynamique. Ce plugin est bas niveau et est destiné à être intégré dans une page web.

## Paradigme

La documentGrid est construite sur le pattern widget de jquery-ui et se comporte donc comme un widget jquery-ui (initialisation, options, évènements, etc.) et est basée sur le plugin datatable de jQuery.

Lors de la création d'une documentGrid le plugin génère un objet d'option approprié pour une dataTable et injecte ensuite cette dataTable dans la page courante.
