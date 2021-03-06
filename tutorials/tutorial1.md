---
title: HTML &ndash; un langage à balises pour structurer les documents
subtitle: Doctype et premières balises
layout: tutorial
---

Le but de ce TD est de comprendre comment sont écrites les pages Web basiques,
aussi appelées pages du Web "1.0" statiques. Une telle page Web contient deux
partie :

1. **HTML** : Le fichier HTML contient la structure de la page et son contenu ;
En plus du texte brute, il donne du sens au texte en indiquant ce qui relève
d'un paragraphe, d'un titre, *etc*, à l'aide de balises (exemple `<p>`,
`<title>`,...);

2. **CSS** : Le fichier CSS est responsable de la mise en page de ces éléments
   (mettre ce paragraphe en rose, utiliser la fonte "Sans Serif" pour ce
   titre,... )

Le navigateur (Firefox, Chrome, Safari, IE/Edge, ...) est le logiciel qui nous
permet de visualiser les pages Web. Le but de ce TD est de démystifier la façon
dont est interprétée ces deux types de fichiers par le navigateur.
Pour cela nous allons réaliser un site dont le rendu correspond au fichier
[target.png]({{site.baseurl}}/assets/target.png), en partant du fichier
[index.txt]({{site.baseurl}}/assets/index.txt), qui contient le contenu quasiment
"brut" du site à réaliser.

Nous allons tout d'abord nous consacrer à préciser la structure (le HTML donc)
que l'on peut ajouter à notre contenu brut. Nous verrons ensuite dans la
[deuxième partie du TD](tutorial2.html) comment atteindre le rendu proposé par
[target.png]({{site.baseurl}}/assets/target.png) en réalisant un fichier CSS.

<!--
utilisons pour consulter les documents disponibles sur le World Wide Web (on
cite principalement Chrome, Firefox et Internet Explorer/Edge).  Il sert
principalement à visualiser via un moteur de rendu des sites dont le contenu est
obtenu par le protocole HTTP.

Internet =/ WWW

  Il s'agit de pages dont le contenu est déjà connu et stocké
sous forme de fichier HTML (par exemple, une base encyclopédique) et que
l'utilisateur va consulter.  Il peut s'agir plus généralement de votre site
internet à vous ou d'un petit site de fan qui n'a pas vocation à être modifier
tous les jours.
-->


## Transformation d'un document texte en un document HTML

Le HTML, qui signifie *HyperText Markup Language* (langage de balisage
d’hypertexte), est donc un langage à balise contenant des liens, dits
*hypertextes*, vers d'autres documents.

Les balises permettent de structurer le document. La plupart des balises
commencent par une *balise ouvrante* `<mabalise>`, puis du *contenu* et
finissent par une *balise fermante*
`</mabalise>`. [Certaines balises](http://www.w3.org/TR/html5/syntax.html#void-elements)
n'acceptent pas de contenu et consistent juste d'une balise ouvrante.

<!--  http://www.w3.org/TR/html5/syntax.html#void-elements -->

**Exemple :**

~~~
<p>Ceci est un paragraphe HTML puisqu'il est entouré des balises 'p' </p>
La balise 'br' du saut de ligne ne prend pas de contenu <br>
~~~
{:.html}



Nous allons commencer par des balises un peu particulières, car elles sont de
type "meta", elles sont plus là pour que le navigateur et le serveur s'entendent
bien lors des transferts. Par exemple nous préciserons l'encodage des fichiers,
le doctype,...  Cela n'est pas très passionnant et nous resterons succinct sur
cet aspect.

Récupérer le fichier [index.txt]({{site.baseurl}}/assets/index.txt) (fichier de
base de travail).

1. Ouvrez le fichier [index.txt]({{site.baseurl}}/assets/index.txt) dans le navigateur.

2. Sauvegardez ce fichier en local en le renommant `index.html`. Ouvrir le
fichier dans un navigateur. Quelles différences observez-vous ?

   <!-- 3. Saut de ligne et commentaires HTML mangées -->


3. Rajoutez votre première balise : Écrivez un titre au document et entourez-le
   des balises ouvrantes `<h1>` et fermant `</h1>` pour signifier que c'est bien
   un titre.
  
3. Notre document `index.html` est bien interprété comme un document HTML par le
navigateur. Cependant que se passe-t-il lorsque l'on teste sa conformité au
standard html à l'aide du validateur http://validator.w3.org/ . Quelles sont les
erreurs indiquées ?

   **Note :** Le HTML5 est un standard, c'est-à-dire un langage complètement
   décrit. N'hésitez pas à jeter un rapide coup d'œil
   [au standard](http://www.w3.org/TR/html5/). Ce document est très technique
   mais complet.

4. Commençons par l'erreur **Unable to Determine Parse Mode!**. La validateur
veut vous dire qu'il ne sait pas dans quel langage est écrit votre document. Il
existe plusieurs standards de "langages HTML" : HTML4, XHTML, HTML5,
.... Aujourd'hui, les gens utilisent majoritairement HTML5 et nous ferons de
même.  
   Pour que le document soit valide et reconnu comme un document HTML 5,
   **ajoutez** la ligne

   ~~~
   <!DOCTYPE html>
   ~~~
   {:.html}
   
   au tout début du fichier. **Retestez** la conformité de votre document.

1. Le validateur nous indique **The character encoding was not declared**.
Spécifier l'encodage des caractères est nécessaire pour que les caractères
spéciaux (accents, œ, ...) de votre page soient bien affichés. Dans notre cas,
nous utiliserons toujours l'encodage UTF-8.  
   **Rajoutez** donc la ligne suivante qui déclare l'encodage dans l'en-tête du
   document juste après le DOCTYPE. **Retestez** la conformité de votre document.

   ~~~
   <meta charset="utf-8">
   ~~~
   {:.html}

   **Note :** Vous avez sûrement rencontré des pages Web avec des **Ã©**, **Ã¨**,
     .... Ceci est dû à une mauvaise détection de l'encodage. En effet, le code
     du caractère **é** en UTF-8 correspond à **Ã©** en `iso-8859-15` (encodage
     encore très utilisé dans Windows).
	 
4. La dernière erreur nous parle d'un élément `head` auquel il manque un `title`.
Corrigez votre page Web en insérant un titre après le `<meta>`.

   ~~~
   <title>Le site non officiel de Chuck Norris</title>
   ~~~
   {:.html}

À ce stade, le validateur indique que le fichier index.html est un document
HTML5 valide.


## Structure standard d'un document HTML

Nous allons utiliser notre navigateur pour "inspecter" notre page internet.
Pour cela nous conseillons Chrome ou Firefox. Appuyer sur la touche F12. Une partie de la page doit maintenant être utilisée
par l'outil de développement. Ce dernier doit présenter deux parties bien distinctes, une dédie au HTML et l'autre...aux CSS.
Ces outils sont fabuleux pour apprendre comment se construisent une page internet. Nous vous conseillons de jouer un peu avec pendant un quart d'heure.
Un clic droit avec la souris sur un élément du html d'une page suivi d'un "Examiner l'élément" vous permettra de jouer avec le HTML et les CSS.

1. Encadrer par les balises `<body>` et `</body>` toute la partie du document se trouvant
en dessous de `</head>`.
2. Insérer une balise `<html>` avant la balise `<head>` et une balise `</html>` après la
balise `</body>`.

Les balises HTML définissent une structure arborescente du document où :

* html est l'élément racine
* head et body sont les deux fils de l'élément html
* title et meta sont deux fils de l'élément head
* "Le site non officiel de Chuck Norris" est un fils de l'élément title.

----------------------

 Cependant   
Voici un squelette de page HTML5 :
   
~~~
<!DOCTYPE html>
<html>
    <head>
        <!-- L'en-tête du document avec au moins un titre -->
        <title></title>
    </head>
    <body>
	   <!-- Le corps du document -->
	</body>
</html>

~~~
{:.html}

La ligne `<!DOCTYPE html>` signifie que le langage du document est HTML5. Le document en lui-même est inclus dans la balise `<html>` et est composé de deux parties :

* l'en-tête contient des informations sur le document HTML
* le corps contient le vrai contenu

<!-- parle-t-on des attributs des balises ? -->

## Les Commentaires en HTML
Il est possible de rajouter des commentaires dans le HTML. Cela n'est pas interpréter par le navigateur, et n'est donc pas visible par l'utilisateur. 
Il s'agit donc d'information laissées par des développeurs pour des développeurs. On les places entre les balises `<!--` et `-->` : 


~~~
<!--Cela est un commentaire dans un fichier HTML  -->
~~~
{:.html}

Il y a justement des commentaires dans le fichier index.html, comme autant de consignes afin de les remplacer par du HTML.
Nous expliciterons ces dernières dans les sections suivantes.

## Titres

Nous allons commencer par rajouter de la structure à notre page.
Pour ce faire nous allons utiliser les balises `<h2>` à `<h3>` pour identifier les différentes sections (`<h1>` est utilisé pour le titre du document).
Si vous cherchez un bon exemple d'utilisation de balises `<h2>`, faites un clic droit sur le titre 'Titres' juste au dessus puis "inspecter l'élément".


<b>Exercice : </b>

Ajouter la balise `<h2>` à ces éléments signifiées par les commentaires : `<!--section -->`. 

Les sous sections `<h3>` sont associés quant à eux aux commentaires : `<!--sous section -->`, ajouter les et recharger la page.


## Éléments de regroupement

### Paragraphes

Utiliser maintenant les balises `<p>` et `</p>` autour des paragraphes du document.
Les paragraphes vous sont signifiés par `<!--début paragraphe -->` et `<!--fin paragraphe -->`. Si vous faites un clic droit inspecter l'élément sur ce paragraphe, 
vous verrez justement que ce texte est dans un paragraphe.


<a name="ul"></a>
### Listes

En HTML nous pouvons faire des listes ordonnées ou pas :

~~~
<ul>
  <li>premier item</li>
  <li>deuxième item</li>
</ul>
<ol>
  <li>premier item</li>
  <li>deuxième item</li>
</ol>
~~~
{:.html}

Ce qui donne une fois interprété par le moteur de rendu du navigateur : 
<ul>
  <li>premier item</li>
  <li>deuxième item</li>
</ul>
<ol>
  <li>premier item</li>
  <li>deuxième item</li>
</ol>

<b>Exercice : </b>

1. Utiliser les balises `<ul>` et `<li>` pour structurer la liste à puces `<!--liste -->` dans index.html. (ne vous soucier pas encore des commentaires <!-- lien externe` pour l'instant )
2. Utiliser les balises `<ol>` et `<li>` pour structurer la liste numérotée `<!--liste numérotée -->` dans index.html.


## Image : un exemple d'élément embarqué


<b>Exercice : </b>
Télécharger l'image [chuck-jeune.jpg]({{site.baseurl}}/assets/chuck-jeune.jpg). Copier là dans un répertoire assets/img 
à partir de votre fichier index.html.
Ajouter la via la balise `<img>` en début de section (voir le fichier [target.png]({{site.baseurl}}/assets/target.png))
en lieu et place du commentaire `<!--l'image de Chuck Young doit être positionnée ici  -->`.

~~~
<img src="./assets/img/chuck-jeune.jpg" alt="Chuck Jeune, la légende est en marche."/>
~~~
{:.html}

Faite de même avec l'image [beware.jpg]({{site.baseurl}}/assets/beware.jpg) : positionner là en lieu et place du commentaire `<!--l'image de Chuck Beware ici   -->`.


src et alt sont des attributs de l'élément img.

L'attribut alt permet d'ajouter un texte alternatif :

 * pour les navigateurs ne pouvant les afficher (navigateur textuel <a href="http://lynx.browser.org/">Lynx</a>)
 * pour les personnes ne peuvent pas bien les voir (aveugles ou déficits visuels légers). 

## Éléments sémantiques


<a name="semantic"></a>

### Liens

L'un des éléments les plus emblématique du HTML est sans doute la balise `<a>`.

Un lien est composé principalement par une url cible et un libellé (qui sera visible par l'utilisateur et souligné en bleu):


~~~
<a href="http:://urlcible.com">le libellé</a>
~~~
{:.html}

 * Dans le cas d'un lien externe, il suffit de renseigner tel quel l'url de la cible : `<a href="http://lynx.browser.org/">Lynx</a>`


 * Dans le cas d'un lien interne, on va utiliser les ancres `#monancre`.
On aura positionné quelque par dans le document  un lien cible :
`<a id="mon_ancre_en_debut_de_fichier"></a>`. Notre lien interne sera 
alors : `<a href="#mon_ancre_en_debut_de_fichier">Retour au haut de page</a>`


Chercher dans votre fichier index.html les commentaires `<!-- lien interne ...` et `<!-- lien externe ...`.
Et remplacer les par des balises `<a>`.

<a id="citation"></a>

### Table 

Les tables.


### Citation

<blockquote > 
Un biscuit ça n'a pas de 'spirit', c'est juste un biscuit. 
Mais avant c'était du lait, des oeufs. Et dans les oeufs, il 
y a la vie potentielle. 

<cite>Jean Claude Van Damme</cite>
</blockquote>

Les citations permettent d'identifier un court texte sur lequel on veut attirer l'attention.
Cela est utilisé notamment pour montrer qu'on a du 'spirit'.

<b>Exercice : </b>


Utiliser la balise `blockquote` et `<cite>` pour mettre en avant la citation en tout début de document (rechercher `<!-- utiliser blockquote ici  -->`).

### Emphase

La balise `<em>` permet de mettre en évidence des passages importants dans un
texte. Identifier les mots en gras dans le document .pdf et les marquer avec cette balise
dans le fichier HTML.

<b>Exercice : </b>

Mettre en emphase la phrase qui suit le commentaire : `<!-- mettre en emphase cette phrase -->`.


## Fini !

Nous en avons fini en ce qui concerne le contenu et la structure de notre site.
Nous savons ajouter de la structure à une page HTML avec les balises spécifiques.


Une remarque peut être informulée de votre part : mais pourquoi le fait de rajouter <h1> a mon titre change effectivement l'apparence des titres ? cela n'est pas à la charge du CSS justement ?
Les navigateurs appliquent des CSS par défaut associés aux balises HTML (exemple : par convention les liens <a> sont en bleus et soulignés sans que l'on est rien à faire).
Cela évite d'avoir justement TOUT à refaire en CSS : des styles par défauts sont proposés.
Dans le TD suivant nous verrons comment améliorer l'aspect du site.

<!--
1. Passer le document sous l'encodage UTF-8 (que nous privilégierons désormais).
2. Travaillez sur votre projet en définissant les structures HTML des pages de votre site Web.
-->
