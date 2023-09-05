# TP Simulation d'une machine & Assembleur


## Un simulateur basique :octicons-gear-24:

On se propose de mettre en pratique les connaissance acquises grâce [au simulateur développé par Peter L. Higgison](https://www.peterhigginson.co.uk/ARMlite/). Ce simulateur est basé sur l'architecture de Von Neumann étudié précédemment, on y retrouve donc un processeur, ses registres et une mémoire.

L'interface de ce simulateur est découpé en quatre grandes parties :

* :fontawesome-solid-code: Le **programme** où vous allez saisir vos différents programmes en assembleur.

* :fontawesome-solid-microchip: Le **processeur** avec l'état de ses différents registres (notamment l'adresse de la prochaine instruction `PC`, ses registres de travail `R0` à `R12`, ses drapeaux `N Z C V`).

* :fontawesome-solid-memory: La **mémoire** dont vous pouvez modifier la représentation des valeurs (hexadécimale, binaire, décimal etc.)

* :material-console: Les **entrées / sorties** qui permet à la machine de communiquer avec le monde extérieur !

!!! note "Des valeurs de 32 bits ?"
    Comme vous pouvez le constater, une cellule de la mémoire du simulateur correspond à 32 bits. La mémoire est pourtant bien découpée en octets, les adresses font bien référence à des octets. On ne pourra hélas utiliser que les adresses divisibles par 4 dans notre programme.


??? question "Questions 1"
    1. Les adresses de la mémoire de cette machine vont de `0x0000`à `0xFFFFF`. Quelle est la taille de la mémoire ?
    
    2. Quelle est la taille en bits d'un registre du processeur dans cette simulation ?

À vos claviers, nous allons manger un peu d'assembleur.

## Un premier programme :material-file-code:

Copier ce programme (bouton EDIT) :

```tasm
    MOV R2, #0xABCD ; (1)!
    MOV R7, #0x1234
    ADD R0, R2, R7 ; (2)!
    HALT ; (3)!
```

1. `R2` :fontawesome-solid-arrow-left: `0xABCD` Le symbole `#` permet de préciser une **valeur immédiate**. `#!tasm MOV` vient du mot anglais **move**, déplacer.

2. `R0` :fontawesome-solid-arrow-left: `R2` + `R7`

3. Permet d'arrêter (ou mettre en pause) l'exécution du programme.

Lorsque le programme est assemblé (bouton SUBMIT), le programme est stocké dans la mémoire, prêt à être exécuté :

    0xe30a2bcd 0xe3017234 0xe0820007 0xe1000070

??? question "Questions 2"
    1. **Exécuter** ce programme (:fontawesome-solid-play:). Que fait ce programme ? Vérifier que le résultat obtenu est correct en passant à une représentation décimale (non-signé).

    2. Sur combien de bits est stockée une instruction ? Quel est le code machine de l'instruction `#!tasm HALT` ?

    3. Que vaut le Compteur de Programme (`PC`) au début et à la fin de l'exécution du programme ? De combien augmente-t-il à chaque étape (:fontawesome-solid-stop: pour reset le simulateur, :fontawesome-solid-forward-step: pour exécuter le programme pas à pas) ? Justifier.

    4. En analysant attentivement le code machine des deux premières instructions `#!tasm MOV` indiquer où se trouve l'information du **registre de destination** et celle de la **valeur immédiate** dans le code machine.

    5. Quelle serait l'instruction pour incrémenter un registre ?


## Déplacer des valeurs entre les registres et la mémoire :material-package-variant-closed:

| Instruction                | Exemples                         | Signification                                                                    |
|----------------------------|----------------------------------|----------------------------------------------------------------------------------|
| `#!tasm MOV R, <Opérande2>` | `#!tasm MOV R0, #25` <br/> `#!tasm MOV R0, R1 ` | `R` :fontawesome-solid-arrow-left: `<Opérande2>` <br/>Permet d'affecter une valeur à un registre,<br/> ou copier un registre dans un autre. |
| `#!tasm LDR R, <Adresse>` | `#!tasm LDR R0, 0xFC` | `R` :fontawesome-solid-arrow-left: `Mémoire[<Adresse>]` <br/> Permet d'affecter une valeur (32 bits) depuis son<br/> un emplacement mémoire à un registre. | 
| `#!tasm STR R, <Adresse>` | `#!tasm STR R1, 120`  | `Mémoire[<Adresse>]` :fontawesome-solid-arrow-left: `R`<br/> Permet d'affecter la valeur d'un registre à<br/> un emplacement de la mémoire. |

??? question "Questions 3"
    1. Écrire un programme qui affecte la valeur 42 à l'emplacement d'adresse `0xA4`. À la fin du programme, la ligne `0x000a` de la mémoire doit être :

        `0x000a           0          42           0           0`


    2. Modifier ce programme pour qu'il affecte ensuite la valeur 13 à l'emplacement suivant : 

        `0x000a           0          42          13           0`

    3. Modifier le programme pour qu'il ensuite échange de place les valeurs de ces deux emplacements. Le programme doit marcher peu importe les valeurs initiales (ici 42 et 13) et peu importe les valeurs courantes des registres :

        `0x000a           0          13          42           0`

    4. Que fait l'instruction `#!tasm LDR R0, .InputNum` ?

!!! note "Adressage indirect"
    Un registre `R` peut stocker une adresse (le registre est alors appelé **pointeur**). On écrit `[R]` pour récupérer la valeur à cette adresse dans la mémoire. Par exemple `#!tasm LDR R0, [R1]` affecte à `R0` la valeur à l'adresse `R1` (et non la valeur de `R1` en elle-même).

## Les labels :fontawesome-solid-tag:

Un **label** (ou étiquette en français) permet de **nommer symboliquement** une adresse. 

```tasm
    MOV R0, #0
mon_label: ;(1)!
    ADD R0, R0, #1
    B mon_label ;(2)!
    HALT
```

1. `mon_label` désigne ici l'adresse de l'instruction suivante </br>`#!tasm ADD R0, R0, #1`, c'est-à-dire `0x04`.

2. `#!tasm B` est un **saut (ou branchement) inconditionnel**, il permet de *sauter* à une instruction particulière grâce à son adresse (`mon_label`).

!!! note "Saut relatif"
    On peut sauter à un label, mais aussi un nombre d'instructions relativement à sa position. Par exemple : `#!tasm B .+3` sautera jusqu'à la 3ème prochaine instruction (en ignorant donc les 2 instructions entre). `#!tasm B .-5` sautera 5 instructions en arrière.


??? question "Questions 4"
    1. Exécuter ce programme pas à pas. Que fait-il ?

    2. Modifier le programme pour utiliser un saut relatif à la place.



## Les conditions et les boucles :material-arrow-decision:

Si les instructions `#!python if` et `#!python while` n'existent pas en assembleur, il existe à la place les **sauts conditionnels**. On **compare** deux valeurs à tester, et suivant le résultat de cette comparaison on **saute** ou non à une ligne de code (grâce à un label ou relativement).

### Comparaison

On **compare** une valeur d'un registre avec une autre valeur grâce à l'instruction `#!asm CMP` (compare). Le résultat de cette comparaison est stocké dans les différents **drapeaux** (`N Z C V`) du processeur.

```tasm
    MOV R0, #10
    CMP R0, #20 ;(1)!
    HALT
```

1. Compare la valeur du registre `R0` avec la valeur immédiate 20.

??? question "Questions 5"
    0. Que valent les drapeaux (*status bits* dans le simulateur) `N Z C V` avant d’exécuter le programme ?

    1. Exécuter ce programme. Noter la valeur des différents drapeaux.
    
    2. De même en modifiant la valeur qui est comparée à `R0` à 5 puis à 10.

    2. Conclure.

### Sauts conditionnels

Une fois les drapeaux modifiés par `#!asm CMP`, on effectue un **saut conditionnel** suivant le résultat de la comparaison grâce aux instructions :

| Instruction | Symbole | Signification |
|:-----------:|:-------:|:--------------|
| `#!tasm BEQ label` | $=$   | **B**ranch if **EQ**qual           |
| `#!tasm BNE label` | $\ne$ | **B**ranch if **N**ot **EQ**qual   |
| `#!tasm BLT label` | $<$   | **B**ranch if **L**ess **T**han    |
| `#!tasm BGT label` | $>$   | **B**ranch if **G**reater **T**han |


Modifions le code de la section précédente, en transformant le saut inconditionnel `#!tasm B` en un saut conditionnel :

```tasm hl_lines="4 5"
    MOV R0, #0
mon_label:
    ADD R0, R0, #1
    CMP R0, #10
    BLT mon_label
    HALT
```

??? question "Questions 6"
    1. Exécuter ce programme pas à pas. Que fait-il ?

    2. Modifier le programme pour faire la multiplication $7 \times 8$ dans le registre `R0`.

    3. Modifier le programme pour qu'il demande deux nombres à l'utilisateur (grâce à `#!tasm LDR R, .InputNum`) et effectue la multiplication de ces deux nombres.

    4. Écrire le programme qui demande un nombre $n$ à l'utilisateur et affiche $n!$ (factorielle). Pour afficher le contenu d'un registre `R` dans la console, on utilise l'instruction `#!tasm STR R, .WriteUnsignedNum`.

## Hello, World! :material-hand-wave:

!!! quote "Raghu Venkatesh"
    If you can write "hello world" you can change the world.

Je n'allais tout de même pas vous apprendre l'assembleur sans vous faire afficher « *Hello, World.* » dans la console ! Pour afficher un message dans la console, il faut d'abord le stocker dans la mémoire :

```tasm
mon_message:
    .ASCIZ "Hello, World!"
```
??? note "Une chaîne de caractères dans la mémoire"

    Regardons la mémoire après avoir assemblé le code précédent :

        0x6c6c6548  0x57202c6f  0x646c726f  0x00000021

    Les caractères sont codés en ASCII donc sur un octet, on découpe ainsi :

        6c 6c 65 48    57 20 2c 6f    64 6c 72 6f    00 00 00 21

    On regarde enfin la table ASCII pour déterminer les caractères correspondants :

        l  l  e  H     W     ,  o     d  l  r  o           \0 ! 

    Pourquoi les caractères sont renversés ? [La notion de boutisme.](https://fr.wikipedia.org/wiki/Boutisme)

On laissera ces données à la fin du programme. On affecte la première adresse de ce message dans un registre, comme `R0`, puis on utilise `#!tasm STR` pour l'envoyer à la console :

```tasm
    MOV R0, #mon_message ;(1)!
    STR R0, .WriteString ;(2)!
    HALT

mon_message:
    .ASCIZ "Hello, World!"
```

1. On copie l'adresse de début de `mon_message`, soit `0xC`.

2. On envoie l'adresse `0xC` à la console qui va ensuite lire le contenu du message.

??? question "Questions 7"
    1. La console ne reçoit que l'adresse du début du message. Or, le message s'étale sur plusieurs emplacements mémoire. [Comment](https://fr.wikipedia.org/wiki/Caract%C3%A8re_nul) la console fait-elle pour savoir quand s'arrêter ?

    2. Écrire le programme qui demande à l'utilisateur son âge et affiche s'il est majeur ou non. 
