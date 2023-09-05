# Introduction

## Python, un langage populaire

**Python** est un langage de programmation inventé par Guido Van Rossum en 1991. C'est un langage très populaire dans l'industrie du numérique (pour le développement d'applications, de sites Web etc.) et le monde scientifique (notamment en intelligence artificielle) de par sa clarté, sa concision et la richesse de ses bibliothèques (du code extérieur permettant d'ajouter d'autres fonctionnalités au langage). Il est aussi très adapté pour l'apprentissage de la programmation. 

## Qu'est-ce un programme ?

### Définition

Un **programme** est une séquence d'instructions qui manipulent des données (nombres, chaînes de caractères, des tableaux, des images etc.). Un programme fera exactement ce que vous lui demandez de faire.

### Langage de programmation, une abstraction

 La machine ne parle pas anglais. Par le biais de son processeur, une machine **exécute** ces instructions codées sous forme binaire. Évidemment, ce serait frustrant de coder directement en binaire (comme à l'époque sur cartes perforées), c'est la raison pour laquelle les langages de programmation ont été inventé pour s'éloigner du code machine et se rapprocher du langage et raisonnement humain.

!!! note "Différence langage de bas/haut niveau"
    * Les langages de **bas niveau**, comme le code machine ou l'assembleur, sont très complexes à utiliser, car très éloignés du langage naturel, on dit que ce sont des langages « proches de la machine », en contrepartie ils permettent de faire des programmes très rapides à l'exécution. Par exemple en assembleur, l'instruction `LD A, 0x03` permet de mettre le nombre 3 dans le registre A du processeur.

    * Les langages de **haut niveau** (C, C++, Java, Python...) sont eux plus faciles à utiliser, car plus proches du langage. Par exemple, l'instruction `i = 12 if b > 3 else 0` en Python. 


!!! note "Notion de langage compilé et interprété"
    Chaque instruction que vous écrivez en Python va être traduit au fur et à mesure de son exécution en code machine, c'est un langage dit **interprété**. D'autres langages comme le C nécessitent de traduirement entièrement le script en langage machine avant son éxecution, c'est un langage **compilé**.

Une machine possède un nombre limité d'**instructions** basiques qui permettent de gérer par exemple des données stockées dans des **variables**, faire des **tests** sur ces variables, **répéter** des instructions etc.


La difficulté en programmation est donc de **traduire** sa façon de penser et de résoudre un problème spécifique en une séquence de ces quelques instructions basiques. Il n'y a pas de lignes de code superflues.


La **syntaxe** souvent rigide de ces instructions est à connaître, la machine hélas ne corrige pas vos erreurs. 