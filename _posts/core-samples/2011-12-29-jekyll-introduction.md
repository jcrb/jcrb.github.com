---
layout: post
category : lessons
tagline: "Supporting tagline"
tags : [intro, beginner, jekyll, tutorial]
---
{% include JB/setup %}

Cette introduction Jekyll décrit exactement ce que Jekyll est et pourquoi vous voudrez l'utiliser.
Immédiatement après l'introduction, nous allons apprendre exactement comment Jekyll fait ce qu'il fait.

## Vue d'ensemble

### Qu'est-ce Jekyll?


Jekyll est un parseur en ruby (gem) utilisé pour construire des sites Web statiques à partir d'éléments dynamiques tels que les modèles, partials, liquid code, markdown, etc. Jekyll est connu comme "un simple blog, générateur de site statique".

### Examples

Ce site est créé avec Jekyll. [Other Jekyll websites](https://github.com/mojombo/jekyll/wiki/Sites).



### Que fait Jekyl?

Jekyll est un gem ruby que vous intallez sur votre système local.
Une fois là, vous pouvez appeler `jekyll --server` sur un répertoire et à condition que ce répertoire soit formatté comme Jekyll l'attend, il va faire des choses magiques somme parser des fichiers Markdown/text, créer des catégories, des tags, des liens et , construire vos pages à partir de modèles de mise en page et partials.

Une fois parsés, Jekyll stocke le résultat dans un dossier autonome statique `_site`.
L'intention ici est que vous pouvez servir tous les contenus de ce dossier de manière statique à partir d'un serveur web statique.

Vous pouvez penser Jekyll comme un blog dynamique normal mais plutôt que d'analyser le contenu à chaque demande, Jekyll fait cela une fois _à priori_ et met en cache la _totalité du site web_ dans un dossier pour le produire de manière statique.

### Jekyll n'est pas un logiciel de Blog

**Jekyll est un parseur.**

Jekyll ne fournit pas de contenu et n'a pas non plus tous les modèles ou éléments de conception.
C'est une source fréquente de confusion au début.
Jekyll ne vient pas avec tout ce que vous utilisez ou voyez sur votre site web - c'est à vous de le faire.

### Why Should I Care?

Jekyll is very minimalistic and very efficient.
The most important thing to realize about Jekyll is that it creates a static representation of your website requiring only a static web-server.
Traditional dynamic blogs like Wordpress require a database and server-side code.
Heavily trafficked dynamic blogs must employ a caching layer that ultimately performs the same job Jekyll sets out to do; serve static content.

Therefore if you like to keep things simple and you prefer the command-line over an admin panel UI then give Jekyll a try.

**Développeurs comme Jekyll parce que nous voulons écrire du contenu comme nous écrivons du code:**

- Possibilité d'écrire du contenu en markdown ou textile dans votre éditeur de texte favori. 
- Possibilité d'écrire et prévisualiser votre contenu via localhost. 
- Pas de connexion Internet nécessaire.
- Possibilité de publier via git.
- Possibilité d'héberger votre blog sur un serveur web statique.
- Possibilité d'héberger sur GitHub.
- Pas de base de données requise.

# Comment Jekyll fonctionne

Ce qui suit est un aperçu complet mais concis de comment fonctionne exactement Jekyll.

Soyez conscient que les concepts de base sont introduits en succession rapide sans exemples de code.
Cette information n'est pas destinée à vous apprendre précisément comment faire quelque chose, mais plutôt
est destiné à vous donner une _Image complète_ de ce qui se passe dans le monde de Jekyll.

L'apprentissage de ces concepts de base devrait vous aider à éviter les frustrations communes et, finalement,vous aider à mieux comprendre les exemples de code contenus tout au long de Jekyll-Bootstrap.


## Configuration initiale

Après avoir [installé jekyll](/index.html#start-now) vous devez formater votre répertoire comme jekyll l'attend.
Jekyll-bootstrap fournit le répertoire de base.

### La strucyure de base de l'application Jekyll

Jekyll s'attend à ce que le répertoire de base soit présenté de la manière suivante:

    .
    |-- _config.yml
    |-- _includes
    |-- _layouts
    |   |-- default.html
    |   |-- post.html
    |-- _posts
    |   |-- 2011-10-25-open-source-is-good.markdown
    |   |-- 2011-04-26-hello-world.markdown
    |-- _site
    |-- index.html
    |-- assets
        |-- css
            |-- style.css
        |-- javascripts


- **\_config.yml**
	Stocke les données de configuration.

- **\_includes**
	Ce répertoire est destiné aux partial views.

- **\_layouts**
	Ce répertoire est pour les principaux modèles utilisés par votre contenu.
	Vous pouvez avoir des configurations différentes pour vos pages et sections.
	
- **\_posts**
	Ce répertoire contient votre contenu dynamique/posts.
	Le nom du fichier doit respecter le formalisme `@YEAR-MONTH-DATE-title.MARKUP@`.

- **\_site**
	C'est là que le site généré sera placé une fois que Jekyll l'a transformé.

- **assets**
	Ce dossier ne fait pas partie de la structure standard de jekyll ..
	Le dossier assets représente _tout dossier générique_ que vous voulez créer dans votre répertoire racine.
	Les répertoires et les fichiers non correctement formatées pour jekyll seront laissés intacts pour votre usage.

(read more: <https://github.com/mojombo/jekyll/wiki/Usage>)


### Jekyll Configuration

Jekyll prend en charge diverses options de configuration qui sont entièrement décrits ici:
(<https://github.com/mojombo/jekyll/wiki/Configuration>)




## Content in Jekyll

Le contenu dans Jekyll est un article ou une page. 
Ces "objects" sont insérés dans un ou plusieurs templates pour construire la page statique qui sera affichée.

### Posts et Pages

Posts et pages doivent être écrits en markdown, textile, ou HTML and peuvent aussi contenir des modèles utilisant la syntaxe Liquid.
Posts et pages peuvent avoir des meta-data requises à chaque page comme title, url path, comme des meta-data personnelles.

### Travailler avec les Posts

**Créer un Post**
Les Posts sont créés en formattant correctement un fichier qui est ensuite placé dans le répertoire `_posts`.

**Formattage**
Un post doit avoir un nom de fichier valide de la forme `ANNEE-MOIS-DATE-titre.MARKUP` et doit être placé dans le répertoire `_posts`.

Si le format est nvalide Jekyll ne reconnait pas le fichier comme étant un post. La date et le titre sont automatiquement parsés à partir du fichier source du Post.

De plus chaque fichier doit avoir une [en-tête YAML](https://github.com/mojombo/jekyll/wiki/YAML-Front-Matter) placée avant son contenu.
L'en-tête YAML est une syntaxe YAML spécifiant les meta-data pour un fichier donné.

**Order**
Ordering is an important part of Jekyll but it is hard to specify a custom ordering strategy.
Only reverse chronological and chronological ordering is supported in Jekyll.

Since the date is hard-coded into the filename format, to change the order, you must change the dates in the filenames.

**Tags**
Posts can have tags associated with them as part of their meta-data.
Tags may be placed on posts by providing them in the post's YAML front matter.
You have access to the post-specific tags in the templates. These tags also get added to the sitewide collection.

**Categories**
Posts may be categorized by providing one or more categories in the YAML front matter.
Categories offer more significance over tags in that they can be reflected in the URL path to the given post.
Note categories in Jekyll work in a specific way.
If you define more than one category you are defining a category hierarchy "set".
Example:

    ---
    title :  Hello World
    categories : [lessons, beginner]
    ---

This defines the category hierarchy "lessons/beginner". Note this is _one category_ node in Jekyll.
You won't find "lessons" and "beginner" as two separate categories unless you define them elsewhere as singular categories.

### Working With Pages

**Creating a Page**
Pages are created by properly formatting a file and placing it anywhere in the root directory or subdirectories that do _not_ start with an underscore.

**Formatting**
In order to register as a Jekyll page the file must contain [YAML Front-Matter](https://github.com/mojombo/jekyll/wiki/YAML-Front-Matter).
Registering a page means 1) that Jekyll will process the page and 2) that the page object will be available in the `site.pages` array for inclusion into your templates.

**Categories and Tags**
Pages do not compute categories nor tags so defining them will have no effect.

**Sub-Directories**
If pages are defined in sub-directories, the path to the page will be reflected in the url.
Example:

    .
    |-- people
        |-- bob
            |-- essay.html

This page will be available at `http://yourdomain.com/people/bob/essay.html`


**Recommended Pages**

- **index.html**
  You will always want to define the root index.html page as this will display on your root URL.
- **404.html**
  Create a root 404.html page and GitHub Pages will serve it as your 404 response.
- **sitemap.html**
  Generating a sitemap is good practice for SEO.
- **about.html**
  A nice about page is easy to do and gives the human perspective to your website.


## Templates in Jekyll

Templates are used to contain a page's or post's content.
All templates have access to a global site object variable: `site` as well as a page object variable: `page`.
The site variable holds all accessible content and metadata relative to the site.
The page variable holds accessible data for the given page or post being rendered at that point.

**Create a Template**
Templates are created by properly formatting a file and placing it in the `_layouts` directory.

**Formatting**
Templates should be coded in HTML and contain YAML Front Matter.
All templates can contain Liquid code to work with your site's data.

**Rending Page/Post Content in a Template**
There is a special variable in all templates named : `content`.
The `content` variable holds the page/post content including any sub-template content previously defined.
Render the content variable wherever you want your main content to be injected into your template:

{% capture text %}...
<body>
  <div id="sidebar"> ... </div>
  <div id="main">
    |.{content}.|
  </div>
</body>
...{% endcapture %}
{% include JB/liquid_raw %}

### Sub-Templates

Sub-templates are exactly templates with the only difference being they
define another "root" layout/template within their YAML Front Matter.
This essentially means a template will render inside of another template.

### Includes
In Jekyll you can define include files by placing them in the `_includes` folder.
Includes are NOT templates, rather they are just code snippets that get included into templates.
In this way, you can treat the code inside includes as if it was native to the parent template.

Any valid template code may be used in includes.


## Using Liquid for Templating

Templating is perhaps the most confusing and frustrating part of Jekyll.
This is mainly due to the fact that Jekyll templates must use the Liquid Templating Language.

### What is Liquid?

[Liquid](https://github.com/Shopify/liquid) is a secure templating language developed by [Shopify](http://shopify.com).
Liquid is designed for end-users to be able to execute logic within template files
without imposing any security risk on the hosting server.

Jekyll uses Liquid to generate the post content within the final page layout structure and as the primary interface for working with
your site and post/page data.

### Why Do We Have to Use Liquid?

GitHub uses Jekyll to power [GitHub Pages](http://pages.github.com/).
GitHub cannot afford to run arbitrary code on their servers so they lock developers down via Liquid.

### Liquid is Not Programmer-Friendly.

The short story is liquid is not real code and its not intended to execute real code.
The point being you can't do jackshit in liquid that hasn't been allowed explicitly by the implementation.
What's more you can only access data-structures that have been explicitly passed to the template.

In Jekyll's case it is not possible to alter what is passed to Liquid without hacking the gem or running custom plugins.
Both of which cannot be supported by GitHub Pages.

As a programmer - this is very frustrating.

But rather than look a gift horse in the mouth we are going to
suck it up and view it as an opportunity to work around limitations and adopt client-side solutions when possible.

**Aside**
My personal stance is to not invest time trying to hack liquid. It's really unnecessary
_from a programmer's_ perspective. That is to say if you have the ability to run custom plugins (i.e. run arbitrary ruby code)
you are better off sticking with ruby. Toward that end I've built [Mustache-with-Jekyll](http://github.com/plusjade/mustache-with-jekyll)


## Static Assets

Static assets are any file in the root or non-underscored subfolders that are not pages.
That is they have no valid YAML Front Matter and are thus not treated as Jekyll Pages.

Static assets should be used for images, css, and javascript files.




## How Jekyll Parses Files

Remember Jekyll is a processing engine. There are two main types of parsing in Jekyll.

- **Content parsing.**
	This is done with textile or markdown.
- **Template parsing.**
  This is done with the liquid templating language.

And thus there are two main types of file formats needed for this parsing.

- **Post and Page files.**
  All content in Jekyll is either a post or a page so valid posts and pages are parsed with markdown or textile.
- **Template files.**
	These files go in `_layouts` folder and contain your blogs **templates**. They should be made in HTML with the help of Liquid syntax.
	Since include files are simply injected into templates they are essentially parsed as if they were native to the template.

**Arbitrary files and folders.**
Files that _are not_ valid pages are treated as static content and pass through
Jekyll untouched and reside on your blog in the exact structure and format they originally existed in.

### Formatting Files for Parsing.

We've outlined the need for valid formatting using **YAML Front Matter**.
Templates, posts, and pages all need to provide valid YAML Front Matter even if the Matter is empty.
This is the only way Jekyll knows you want the file processed.

YAML Front Matter must be prepended to the top of template/post/page files:

    ---
    layout: post
    category : pages
    tags : [how-to, jekyll]
    ---

    ... contents ...

Three hyphens on a new line start the Front-Matter block and three hyphens on a new line end the block.
The data inside the block must be valid YAML.

Configuration parameters for YAML Front-Matter is outlined here:
[A comprehensive explanation of YAML Front Matter](https://github.com/mojombo/jekyll/wiki/YAML-Front-Matter)

#### Defining Layouts for Posts and Templates Parsing.

The `layout` parameter in the YAML Front Matter defines the template file for which the given post or template should be injected into.
If a template file specifies its own layout, it is effectively being used as a `sub-template.`
That is to say loading a post file into a template file that refers to another template file with work in the way you'd expect; as a nested sub-template.





## How Jekyll Generates the Final Static Files.

Ultimately, Jekyll's job is to generate a static representation of your website.
The following is an outline of how that's done:

1. **Jekyll collects data.**
  Jekyll scans the posts directory and collects all posts files as post objects. It then scans the layout assets and collects those and finally scans other directories in search of pages.

2. **Jekyll computes data.**
  Jekyll takes these objects, computes metadata (permalinks, tags, categories, titles, dates) from them and constructs one
  big `site` object that holds all the posts, pages, layouts, and respective metadata.
  At this stage your site is one big computed ruby object.

3. **Jekyll liquifies posts and templates.**
  Next jekyll loops through each post file and converts (through markdown or textile) and **liquifies** the post inside of its respective layout(s).
  Once the post is parsed and liquified inside the the proper layout structure, the layout itself is "liquified".
	**Liquification** is defined as follows: Jekyll initiates a Liquid template, and passes a simpler hash representation of the ruby site object as well as a simpler
  hash representation of the ruby post object. These simplified data structures are what you have access to in the templates.

3. **Jekyll generates output.**
	Finally the liquid templates are "rendered", thereby processing any liquid syntax provided in the templates
	and saving the final, static representation of the file.

**Notes.**
Because Jekyll computes the entire site in one fell swoop, each template is given access to
a global `site` hash that contains useful data. It is this data that you'll iterate through and format
using the Liquid tags and filters in order to render it onto a given page.

Remember, in Jekyll you are an end-user. Your API has only two components:

1. The manner in which you setup your directory.
2. The liquid syntax and variables passed into the liquid templates.

All the data objects available to you in the templates via Liquid are outlined in the **API Section** of Jekyll-Bootstrap.
You can also read the original documentation here: <https://github.com/mojombo/jekyll/wiki/Template-Data>

## Conclusion

I hope this paints a clearer picture of what Jekyll is doing and why it works the way it does.
As noted, our main programming constraint is the fact that our API is limited to what is accessible via Liquid and Liquid only.

Jekyll-bootstrap is intended to provide helper methods and strategies aimed at making it more intuitive and easier to work with Jekyll =)

**Thank you** for reading this far.

## Next Steps

Please take a look at [{{ site.categories.api.first.title }}]({{ BASE_PATH }}{{ site.categories.api.first.url }})
or jump right into [Usage]({{ BASE_PATH }}{{ site.categories.usage.first.url }}) if you'd like.