# Syle (CSS) {#document-grid-ref:08f82a45-776d-4d92-9a97-69eddc735435}

Le plugin docGrid utilise plusieurs éléments de CSS :

* la classe `overlay` est appliquée à l'ensemble des éléments `<a>` qui sont destinés à être ouvert dans un overlay,
* les éléments représentant l'ouverture d'un document possèdent la classe `openDoc`,
* les éléments représentant un attribut color sont dans une `<div class="colorElement"/>`,
* les éléments ayant un premier niveau de multiplicité sont dans `<span class="multiple firstLevel"/>`,
* les éléments ayant un second niveau de multiplicité sont dans `<span class="multiple secondLevel"/>`,
* les éléments de filtrages sont des `<input class="filter"/>`, ceux de type textuel et relation ont de surcroit la classe *textFilter* (ce qui donne `<input class="filter textFilter"/>`), ceux de type énuméré ont la classe *enumFilter* (ce qui donne `<input class="filter enumFilter"/>`)

