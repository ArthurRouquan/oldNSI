# Le modèle d'architecture séquentielle (Von Neumann)

## Introduction

### Les deux éléments constitutifs de toute machine

Une machine manipule des **données**. Une machine est donc constituée de deux éléments principaux :

* :fontawesome-solid-memory: La **mémoire** (RAM) qui **stocke** les données, dont les programmes dans le modèle de Von Neumann.

* :fontawesome-solid-microchip: Le **processeur** (CPU) qui **traite** les données (addition, soustraction, et logique, etc.).

![Schéma résumé](images/archi_simple_light.png#only-light){ align=center }
![Schéma résumé](images/archi_simple_dark.png#only-dark){ align=center}

### Le cycle instruction :fontawesome-solid-arrows-spin:

Le cycle de base d'une **machine séquentielle** est le suivant :

1. Le processeur **récupère** l'**instruction** à exécuter en mémoire

2. Le processeur décode et **exécute** l'instruction

3. Le processeur **passe** à l'instruction suivante et ainsi de suite

[Pour plus de détails.](https://en.wikipedia.org/wiki/Instruction_cycle)

## La mémoire :fontawesome-solid-memory:

La mémoire est un simple tableau découpé en octets dont les indices sont appelées **adresses**. Elle est aussi appelée **mémoire vive**, ou encore **RAM** pour **R**andom **A**ccess **M**emory, car l'accès à une valeur à une adresse arbitraire est immédiat (de complexité constante).

![Schéma résumé](images/memory_light.png#only-light){ align=center }
![Schéma résumé](images/memory_dark.png#only-dark){ align=center}

??? note "La taille des adresses"
    Une machine est dite 32 bits si une adresse s'écrit sur 32 bits. On peut donc adresser $2^{32}$ valeurs (octets). La taille maximale d'une telle mémoire est donc de $2^{32}$ octets, soit $8 \cdot 2^{32}$ bits, soit 4 Gio.

    Aujourd'hui les machines sont généralement 64 bits. Quelle serait la taille maximale d'une telle mémoire ?

    Les adresses d'une GameBoy sont codées sur 16 bits. Quelle serait la taille maximale d'une telle mémoire ?

Les données sont transférées entre la processeur et la mémoire via un **bus**.

## Le processeur :fontawesome-solid-microchip:
 
### Les registres :octicons-apps-16:

??? note "Le besoin d'une mémoire de travail"

    Imaginons les 4 instructions suivantes :

    1. Lire l’octet à l’adresse 
    `0x781A` :fontawesome-solid-arrow-right: {==42==}

    2. Lire l’octet à l’adresse `0xEF01` :fontawesome-solid-arrow-right: {==24==}

    3. Additionner ces deux valeurs :fontawesome-solid-arrow-right: {==66==}

    4. Écrire le résultat à l'adresse `0x1123`

    Où sont stockées temporairement les {==valeurs lues==} et {==la somme calculée==} ? Dans la petite mémoire de travail intégrée au processeur, les **registres** !

Le processeur possède un petit nombre de cases mémoires rapides appelées **registres** qui lui permet de stocker temporairement des données pour les manipuler.

??? note "Les registres d'une GameBoy"

    Par exemple, le processeur d'une GameBoy possède 7 registres principaux d'un octet chacun, nommés `A`, `B`, `C`, `D`, `E`, `H` et `L`. Le programme précédent peut s'écrire plus précisément :

    1. Lire l'octet à l'adresse `0x781A` et l'affecter au registre `A`

    2. Lire l'octet à l'adresse `0xEF01` et l'affecter au le registre `B`

    3. Ajouter la valeur du registre `B` à la valeur du registre `A`

    4. Écrire la valeur du registre `A` à l'adresse `0x1123`

Un processeur stocke aussi l'**adresse** de l'instruction en cours d’exécution (ou la suivante selon l'architecture) dans le registre `PC` (*Program Counter* en anglais, ou **compteur ordinal** en français) et cette instruction en elle-même dans le registre `IR` (ou `CIR` pour *Current Instruction Register*, le **Registre d'Instruction**).

### Les deux unités ALU et CU :material-calculator-variant: :fontawesome-solid-arrow-down-wide-short:

Un processeur peut être décomposée en deux unités :

* :material-calculator-variant: **L’Unité Arithmétique et Logique (ALU)** permet de réaliser un petit nombre d’opérations simples (addition, soustraction, opérateurs logiques, comparisons etc.). Le résultat de ces opérations est stocké dans un registre appelé **accumulateur** (souvent le registre `A`).


* :fontawesome-solid-arrow-down-wide-short: **L’Unité de Commande (CU)** organise le flot de séquencement des instructions. Il gère par exemple le registre `PC` et `IR`, la récupération des instructions, les instructions de saut etc.

## Résumé

![Schéma résumé](images/archi_light.png#only-light){ align=center }
![Schéma résumé](images/archi_dark.png#only-dark){ align=center }


## Les instructions

### Code opération

Une **instruction** est un simple mot binaire codé sur un ou plusieurs octets. Par exemple, si le processeur de la GameBoy lit l'instruction `00111100` (*opcode*, ou **code opération**), il exécutera "Augmenter de 1 le registre `A`". Chaque type de processeur interprète donc ces mots binaires suivant sa propre architecture et l'agencement de ses transistors.

Le **jeu d'instructions** est l'ensemble des instructions qu'un processeur peut exécuter. Par exemple, les instructions du processeur DMG-01 de la GameBoy sont [disponibles ici](https://www.pastraiser.com/cpu/gameboy/gameboy_opcodes.html).

### L'assembleur

On peut associer au code binaire des instructions un **code mnémonique**. Par exemple, le code opération `00111100` peut se lire plus facilement comme `#!asm INC A` (incrémenter le registre `A`). C'est **l'assembleur**, le langage de plus bas niveau qui représente le langage machine sous une forme lisible par un humain. 

??? note "Code Pokémon Bleu"
    Par exemple, on peut récupérer quelques instructions du code du jeu Pokémon Bleu :

    `00011010 00100010 00010011 01111000` (ou en hexadécimal `0x1A 0x22 0x13 0x03 0x78`)

    Ce qui correspond au code assembleur suivant :

    ```asm
    LD A, (DE) # (1)!
    LD (HL+), A # (2)!
    INC DE # (3)!
    DEC BC # (4)!
    LD A, B # (5)!
    ```

    1. On lit l'octet à l'adresse `DE` (une adresse de 16 bits) dans la mémoire et on l'affecte au registre `A`. On remarque que la GameBoy peut combiner deux registres d'un octet pour former un registre de 16 bits ! `LD` veut dire **Load**, charger.

    2. On affecte la valeur du registre `A` dans la mémoire à l'adresse `HL`, on incrémente le registre `HL` ensuite.

    3. On incrémente le registre `DE`.

    4. On décrémente le registre `BC`.

    5. On affecte `B` à `A`. 

    Ce qui est bien plus compréhensible !

Le langage assembleur permet notamment d'écrire les valeurs manipulées en base décimale, de nommer les adresses (similaire au nom d'une variable !), d'agencer des sections etc. Le **programme assembleur** convertit alors ce code en code machine de façon quasi-immédiate.

### Opérandes

Les opérandes désignent les **entrées** des instructions, par exemple l'opération `#!asm LD` (**Load**, l'affectation) demande deux opérandes sous la forme `#!asm LD OP1, OP2`, ce qui correspond à affecter `OP2` à `OP1`.


`OP1` peut désigner un registre, une valeur dans la mémoire (grâce à son adresse) etc. Si `OP2` peut être un registre ou un emplacement mémoire, elle peut aussi désigner une **valeur immédiate**, c'est-à-dire une valeur qui est soit dans l'instruction-machine en elle-même ou une valeur qui suit immédiatement l'instruction (dépend de l'architecture).

??? note "Adressage indirect"
    Une valeur peut être **déréférencée** pour qu'elle soit interprétée comme une adresse. Par exemple, un registre peut contenir une adresse, on dit alors qu'il est un **pointeur**, car il pointe vers un emplacement mémoire. On peut alors accéder à la valeur à cette adresse grâce au déréférencement :

    ```asm
        LD A, B    #(1)!
        LD A, (B)  #(2)!
    ```

    1. On affecte à `A`, la valeur `B`.

    2. On affecte à `A`, la valeur à l'emplacement d'adresse `B`.


