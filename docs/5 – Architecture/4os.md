---
icon: material/linux
---

# Les systèmes d'exploitation

## Définition :material-linux: :material-microsoft-windows: :material-apple: 

Un **système d'exploitation** (ou Operating System, **OS**) est un logiciel système, un ensemble de programmes, qui sert d'intermédiaire entre les applications (les programmes, le software) et les différents composants matériels d'une machine (le hardware), tel que le processeur, la mémoire, les disques durs, les périphériques entrée/sortie etc.

L'OS fournit ainsi une interface abstraite et standardisée aux applications. Cette interface leur permet de communiquer avec le matériel sans avoir besoin de prendre en compte les détails spécifiques de ce dernier.

Au démarrage de la machine, l'OS est le premier programme à être exécuté et le seul à rester en permanence en exécution, c'est le « chef d'orchestre » de tous les programmes.

Windows, Linux, Android, MacOS et iOS sont les systèmes d'exploitation les plus utilisés à ce jour. 

<figure markdown>
  ![](images/market.png#only-dark){ width="400" }
  ![](images/market-light.png#only-light){ width="400" }
  <figcaption>Parts de marché des systèmes d'exploitation (Février 2023)</figcaption>
</figure>


## Le noyau :fontawesome-solid-heart:

Le **noyau** (ou kernel) est une composante centrale du système d'exploitation qui assure la gestion des ressources matérielles et logicielles de l'ordinateur. Le kernel est responsable de l'interaction directe avec le hardware de l'ordinateur.

![](images/os.png#only-dark)
![](images/os-light.png#only-light)

Quelques-unes des principales fonctionnalités du noyau :

| Fonctionnalité                           | Description                                                                                                                                                                |
| ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Gestion de la mémoire**                | Gère la mémoire RAM allouée aux programmes en cours d'exécution.                                                                                                           |
| **Gestion des processus et des threads** | Permet l'exécution simultanée de plusieurs programmes (processus) en répartissant les tâches à exécuter par le processeur.                                                 |
| **Gestion des entrées/sorties**          | Permet aux  programmes en cours d'exécution de communiquer de manière contrôlée avec les périphériques matériels (clavier, mémoire de stockage, carte réseau, écran etc.). |
| **Gestion des droits**                   | Gère les droits d'accès aux ressources système et aux fichiers.                                                                                                            |

Outre le noyau, un système d'exploitation est constitué de plusieurs composants clés, comme la **gestion des fichiers**, les bibliothèques système, les utilitaires système, l'**interface graphique utilisateur (GUI)** etc.


??? note "Les appels système"
    
    Afin de rendre moins abstrait la relation entre les programmes et le système d'exploitation, analysons ce petit programme en C :

    <div align="center">
    <table>
    <tr>
    <th align="center">Code source</th>
    <th align="center">Code compilé</th>
    </tr>
    <tr>
    <td>

    ```C hl_lines="5"
    #include <cstdio>

    int main()
    {
        printf("Hello, World.");
    }
    ```

    </td>
    <td>

    ```asm hl_lines="8"
    .LC0:
            .string "Hello, World."
    main:
            push    rbp
            mov     rbp, rsp
            mov     edi, OFFSET FLAT:.LC0
            mov     eax, 0
            call    printf
            mov     eax, 0
            pop     rbp
            ret
    ```

    </td>
    </tr>
    </table>
    </div align="center">

    L'instruction qui est en charge d'afficher le message dans la console `#!asm call printf` est ce que l'on nomme un **appel système**, le programme appelle ici la fonction `printf` fournie par l'OS. Un appel système permet au programme de demander à l'OS un service spécifique, tel qu'afficher un message avec `printf`, allouer de la mémoire avec `malloc`, ouvrir un fichier avec `fopen`, créer un processus etc. 

## Histoire des systèmes d'exploitation

Deux excellentes vidéos réalisées par l'Institut Mines-Télécom :

* [Genèse des systèmes d'exploitation](https://youtu.be/4OhUDAtmAUo)

* [L'histoire d'UNIX](https://youtu.be/Za6vGTLp-wg)


## Système d'exploitation libre et propriétaire

On distingue deux types de logiciels :

* Les **logiciels propriétaires** dont le code source est la propriété exclusive de l'entreprise ou de l'individu qui l'a créé. Les utilisateurs n'ont pas accès au code source du logiciel, ils ne peuvent donc ni le modifier, ni examiner ce que fait précisément le logiciel en arrière-plan. Ces logiciels sont généralement payants. 

* Le code source d'un **logiciel libre** est en revanche disponible publiquement. Les utilisateurs peuvent légalement l'utiliser à n'importe quelle fin, l'étudier, le copier, le modifier et le distribuer librement. Ils peuvent aussi contribuer à l'amélioration du logiciel en apportant des modifications à son code source, en signalant et en résolvant des problèmes etc. ce qui profite à l'ensemble de la communauté des utilisateurs du logiciel libre.

Windows, MacOS, iOS, Android sont des systèmes d'exploitation propriétaires. Linux, OpenBSD, Ubuntu, Debian, LineageOS etc. sont des exemples de systèmes d'exploitation libres.

