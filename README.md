
## Arborescence des dossiers et fichiers

La commande intervient dans le cadre d'un dossier qui doit respecter une certaine structure.
Il y a cependant plusieurs options pour gérer les cas simples et plus complexes.
Dans tous les cas, on commence à décrire l'architecture à partir d'un **dossier racine**.
Celui-ci peut être créé pour un cours ponctuel
(une journée de cours avec un seul support de présentation)
ou une série de cours
(plusieurs dizaines d'interventions réparties sur plusieurs semaines avec de nombreux supports).

En dessous de ce dossier racine se trouvent :
- un dossier `dist` qui contient les résultats de la transformations des fichiers sources ;
- un dossier `src` qui contient les fichiers de travail servant à produire le support final ;
- un fichier optionnel `messlides_config.yml` pour configurer l'outil de génération des supports.

Le dossier `dist` reprend la structure du dossier `src` mais ne garde que les fichiers
produits par l'outil de génération ainsi que les « pièces-jointe », en général des images.

Le dossier `src` offre deux options :
1. La première consiste à placer ses fichiers de cours directement dedans,
avec les fichiers attachés. La génération du support (unique dans ce cas)
sera placé directement sous le dossier `dist`.
1. La deuxième consiste à créer un sous-dossier pour séparer les supports de cours.
La génération prendra en compte ce sous-dossier dans le placement du support dans le dossier `dist`.

Voici un exemple d'arborescence utilisant les deux options du dossier `src`.

- dossier racine
    - node_modules # si la commande/package est installée en local
    - dist
        - cours_1
            - slides.html
            - image.[png|svg|jpg|etc...]
        - slides_à_la_racine.html
        - image_à_la_racine.[png|svg|jpg|etc...]
    - src
        - cours_1
            - .ignoremesslides # n'est pas inclu si on appelle build avec un blob pattern
            - slides.[html|md]
            - image.[png|svg|jpg|etc...]
        - slides_à_la_racine.[html|md]
        - theme.css
        - image_à_la_racine.[png|svg|jpg|etc...]
    - messlides_config.yml
    - package.json # si la commande/package est installée en local



## Utilisation de la commande de génération des slides

En fonction de la méthode d'installation :

```bash
# Installation locale (npm install messlides)
./node_modules/.bin/messlides ...
npm run messlides ...

# Installation globale (npm install --globale messlides)
messlides ...

# Avec NPX
npx messlides ...
```

Sous-commande disponibles :

```bash
# build one course
messlides build [-v,--verbose] ./src/cours_1/slides.html [-f,--format=html|pdf]

# build many courses
messlides build [-v,--verbose] ./src/*/slides.html [-f,--format=html|pdf] [--ignore=<PATTERN>]

# launch local http static server
messlides run [-w,--watch] ./src/cours_1/slides.html
messlides run [-w,--watch] ./dist/

# create the directory and copy the default template file
messlides init [-v,--verbose] [--html,--markdown,--md] ./src/cours_2

npx messlides bootstrap [name]
```



## Options de configuration disponibles

```yaml
default_slide_name: "_slides"
default_template_file: "./path/to/template"
theme_file: "./path/to/template"
```



## Tâches

- [ ] Réécrire le script build_course
