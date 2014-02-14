---
layout: post
title: "Créer un blog avec Knitr et Jekyll"
description: ""
category: r
tags: [knitr, jekyll, tutorial]
---
{% include JB/setup %}

Le package knitr package permet de créer facilement un post pour un site géré par Jekyll. Le seul élément nécessaire est un fichier source écrit avec R Markdown.
Le nom de se fichier doit obligatoirement commencer par une date au format AAAA-mm-jj et se terminer par le suffixe Rmd.Les étapes sont les suivantes:

Etape 1
-------
Créer un blog avec Jekyll-Boostrap si vous n'en possédez pas. Un tutoriel succint est disponible (ici)[http://jfisher-usgs.github.com/lessons/2012/05/30/jekyll-build-on-windows/]

Etape 2
-------

Ouvrez une console R et saississez le source suivant
```
KnitPost <- function(input, base.url = "/") {
    require(knitr)
    opts_knit$set(base.url = base.url)
    fig.path <- paste0("figs/", sub(".Rmd$", "", basename(input)), "/")
    opts_chunk$set(fig.path = fig.path)
    opts_chunk$set(fig.cap = "center")
    render_jekyll()
    knit(input, envir = parent.frame())
}
KnitPost("2012-07-03-knitr-jekyll.Rmd")
```

Etape 3
--------

Déplacez le résultat 2012-07-03-knitr-jekyll et le fichier Markdown 2012-07-03-knitr-jekyll.md dans le dépot **git** local jfisher-usgs.github.com.

La fonction *KnitPost* suppose que les images sont placées dans le dossier *figs* situé à la racine du répertoire.

Etape 4
--------

Ajoutez le code CSS suivant au fichier /assets/themes/twitter-2.0/css/bootstrap.min.css pour centrer les images:

[alt=center] {
  display: block;
  margin: auto;
}

Etape 5
-------
en mode console, mettre à jour le blog:
```
cd Documents/Blog/Blog$ cd CreateBlog/jcrb.github.com
~/Documents/Blog/jcrb.github.com$ git add .
~/Documents/Blog/jcrb.github.com$ git commit -m "add new content"
~/Documents/Blog/jcrb.github.com$ git push origin master
```

source
------
http://jfisher-usgs.github.io/r/2012/07/03/knitr-jekyll/, Blog with Knitr and Jekyll
Published: 2012-07-03 par Jason C Fisher


