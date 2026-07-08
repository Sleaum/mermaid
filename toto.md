# Migration des JCL vers les SHELL

## Généralité sur les JCL

### Structure d’un JCL
Pour consulter les JCL, le mieux est d’utiliser [Alex]()
Un job JCL est composé d’un fichier finissant en X.
Chaque phase est défini dans un fichier S. 
Dans les JCL de production, des fichiers C,L et F sont utilisés notamment pour la sauvegarde/restauration


#### Les 4 types de phase
    - batch
    Une phase de type batch execute un programme cobol
    ```
    exemple de code batch
    ```
    - tri
    Une phase de type tri réorganise le contenu du fichier en fonction de critères
    ```
    exemple de code tri 
    ```
    - fusion
    Une phase de type fusion prend en entrée plusieurs fichiers et retourne un seul fichier
    ```
    exemple de code fusion
    ```
    - tri fusion
    Une phase de type fusion réalise une phase tri et fusion en une seule phase

#### Les sauvegardes/restaurations
Si un job ne se passe pas correctement, il faut pouvoir remettre les données modifiés dans leur état initial.
Les données peut être sous forme de fichier ou dans la bdd postgre
- sauvegarde
La 1ère phase du job (C) sauvegarde les fichiers en les copiant vers des fichiers temporaires [et sauvegarde la bdd en créant un snapshot de la bdd identifiable par un marqueur appelé emaj]
- restauration
Lors de la dernière phase du job (F), si un problème est apparu, on restaure les fichiers en copiant les fichiers temporaires de la phase C vers les fichiers modifiés en erreur
#### Les archivages
L’archivage est une opération de stockage pour garder une sauvegarde des fichiers après la fin du graph
#### Les transferts
Les transferts sont des échanges de fichier avec les partenaires. Concrétement, les shells déposent ou récupèrent des fichiers dans un répertoire prédéfini
[le document de didier]()

### Les JCL non migrés
mise en forme du mail de christophe envoyé par Krunal le 08/07/2026
- Liste des chaines non migrées
    - Liste des chaines obsolètes
    - Liste des jobs obsolètes
        - Liste des jobs de correction
        - Liste des jobs one shot

## Généralité sur les SHELL

### Leonard
[Leonard](http://https://leonard.appli.impots/leonard/) est le Saas de référence pour les JCL/Shell

### Gitlab
[Gitlab]() contient la base de code pour le projet medocdb:
- [shell]()
- [lib shell]()
- [composant]()
- [programme]()
…

#### Anatomie d’un dépot
un dépot shell contient:
```
$ tree 
.
├──.gitlab-ci.yml                       # lance les pipelines lors d’un commit
├── CEEDO15X.sh                         # c’est le job
├── launch_rpmbuild.sh                  # génère le rpm sur le nexus
├── launch_tbeb.sh                      #
├── launch_tir_a_blanc.sh               # test avant génération rpm
├── post_phases_CEEDO15X.sh             # appelé par le job. C’est ici qu’on ajoute le code non métier avant l’exécution des phases
├── pre_phases_CEEDO15X.sh              # appelé par le job. C’est ici qu’on ajoute le code non métier après l’exécution des phases 
├── README.md                           #
└── rpmbuild
    ├── SOURCES
    └── SPECS
        └── mdb-shell-ceedo15x.spec     # Contient le changelog, la version, la realase et le palier 
```


#### Cycle de vie d’un dépot
#### Branche
#### Nexus
#### BTW

### SHELL

#### template
#### 4 types de phase
#### Focus gcsort, sprog

## Conversion JCL vers SHELL

copié la ctp novae

## Assemblage

comment les shells s assemble avec ops/launcher et programme et transfert

## Double maintenance

ip api de connexion change
mise à jour des shells source, test, cycle
