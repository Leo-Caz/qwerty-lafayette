+++
title = "Lexique"
+++

<style>
  dt { font-weight: bold; }
  dd p { margin: 0.2em 0; }
  code { font-family: monospace; }
</style>

**🚧 en construction**


Ergonomie & Optimisation
--------------------------------------------------------------------------------

SFU (“Same Finger Usage”), SFB (“Same Finger Bigram”)

: ou « digramme de même doigt ». Quand deux lettres s’enchaînent avec un même
doigt, ce qui est source d’inconfort ou d’erreurs, notamment à haute vitesse.
 
SKU (“Same Key Usage”), SKB (“Same Key Bigram”)

: une répétition de même touche, e.g. pour produire `nn` avec n’importe quelle
disposition de clavier, ou `és` en Ergo‑L.

Extension

: quand un doigt doit atteindre une touche qui est soit sur une autre colonne
que la position de repos, soit à une distance supérieure à une touche.

Ciseau

: quand un bigramme nécessite un changement de rangée inconfortable

Roulement intérieur

: deux touches ou plus enchaînées sur une même main, dans le sens de
l’auriculaire vers l’index. C’est considéré comme l’enchaînement le plus
confortable qui soit.

Roulement extérieur

: deux touches ou plus enchaînées sur une même main, dans le sens de l’index
vers l’auriculaire.

Redirection

: trois touches enchaînées sur une même main avec un changement de direction,
e.g. [D]{.kbd}[S]{.kbd}[F]{.kbd} ou [K]{.kbd}[J]{.kbd}[L]{.kbd} en Azerty ou
Qwerty.

Mauvaise redirection

: une redirection où l’index n’intervient pas. L’un des pires enchaînements
faisables sur un clavier, sinon le pire.


Support logiciel
--------------------------------------------------------------------------------

Scan code

: Données envoyées par un clavier physique à un ordinateur pour lorsque l’on
appuie ou relâche une touche. Suite aux évolutions technologiques (PS/2, USB,
etc.), il existe plusieurs ensembles de scan codes.

: Souvent associé au seul code envoyé lors de la _pression_ d’une touche, en
particulier avec les scan codes « XT » ou « ensemble 1 ». Il permet alors
d’identifier la touche qui a été pressée dans un périphérique de saisie, au plus
bas niveau de l’OS.

Key code

: Code identifiant une touche sur un clavier. Ce code est propre à chaque
système d’exploitation. Ce dernier se charge de convertir les différentes
conventions de _scan codes_ en _key code_, permettant ainsi de faire abstraction
de la technologie du clavier et ainsi développer des dispositions de clavier.

Modificateur

: TODO

Couche (layer)

: TODO

Touche morte (dead key)

: TODO

### Windows

AHK

: TODO

KLC

: TODO

MSKLC

: TODO

Virtual Key (VK, touche virtuelle)

: Code de touche spécifique à Windows, de plus haut niveau que le key code.
Il est utilisé pour définir le placement des touches spéciales ainsi que le
comportement d’une touche lorsqu’elle est utilisée dans un raccourci clavier.


### macOS

keylayout

: TODO

Karabiner

: TODO


### Linux

[X11]

: X est un protocole de système de fenêtrage. [X11] en est la onzième version
majeure.

[X11]: https://fr.wikipedia.org/wiki/X_Window_System

[X.Org]

: Le principal [serveur X][X11] utilisé sur Linux.

[X.Org]: https://fr.wikipedia.org/wiki/X.Org

Wayland

: Un protocole de système de fenêtrage, destiné à remplacer X11 qui n’est plus
maintenu. Bien qu’en développement depuis 2008, son implémentation dans les
environnements de bureau majeurs n’a commencé à être suffisante que dans les
années 2020.

[Wayland]: https://fr.wikipedia.org/wiki/Wayland

XKB (_X_ <em>K</em>eyboard <em>E</em>xtension)

: Un _[protocole][XKB protocol]_ défini comme extension de X11 et dédié à la gestion des
claviers.

: C’est aussi utilisé pour le [_format_ texte de configuration][XKB text format]
des dispositions clavier.

: Par abus de langage c'est aussi la base de données des configurations clavier,
[`xkeyboard-config`][xkeyboard-config].

[XKB protocol]: https://www.x.org/releases/current/doc/kbproto/xkbproto.html
[XKB text format]: https://xkbcommon.org/doc/current/keymap-text-format-v1.html
[xkeyboard-config]: https://gitlab.freedesktop.org/xkeyboard-config/xkeyboard-config

Compose

: Une méthode de saisie (<em lang="en">input method</em> ou IM). C’est notamment
ce qui permet aux touches mortes système (autres que `1dk`) de fonctionner.

: Une [touche][touche Compose] qui permet de 

[touche Compose]: https://fr.wikipedia.org/wiki/Touche_de_composition

XCompose

: Une [spécification][XCompose] de Compose pour les systèmes basés sur X11 et
Wayland. Il existe plusieurs implémentations: `XIM` (référence), `xkbcommon`,
`Gtk`, `Qt`, `ibus`, etc. Notez qu’il existe des différences entre ces
implémentations.

: Un format pour configuer la méthode de saisie XCompose.

: Les fichiers de configuration correspondant. En particulier :
  - `/usr/share/X11/locale/**/Compose` : les fichiers système, organisés par
    locale.
  - `~/.XCompose` : le fichier utilisateur par défaut.

[XCompose]: https://linux.die.net/man/3/xcompose

#### XKB

Keycode

: Code identifiant une touche physique sur un clavier. Le code _brut_ (raw
keycode) est le code numérique issu du traitement bas niveau par le noyau, alors
que le code _symbolique_ est le nom donné dans les fichiers XKB pour faciliter
la configuration haut niveau du clavier. On distingera le code brut du _noyau_
de celui de XKB, ce dernier étant obtenu en ajoutant 8 au premier.
Exemple : sur un clavier QWERTY, le code brut noyau de la touche `Q` est
`16`[^code-brut-noyau], le code brut sur XKB est `16 + 8 = 24` et son code
symbolique est `AD01`[^code-symbolique-iso-9995].
Notez qu’un clavier QWERTY et un clavier AZERTY produisent habituellement des
keycodes identiques pour les touches situées au même emplacement : ainsi la
touche imprimée `Q` sur le clavier QWERTY produira le même keycode que la touche
imprimée `A` sur un clavier imprimé AZERTY. En effet, c’est la configuration du
clavier dans XKB et non le clavier lui-même qui défini la correspondance touche-
keysym.

[ISO/IEC 9995-2]: https://en.wikipedia.org/wiki/ISO/IEC_9995#ISO/IEC_9995-2
[input-event-codes.h]: https://github.com/torvalds/linux/blob/90d35da658da8cff0d4ecbb5113f5fac9d00eb72/include/uapi/linux/input-event-codes.h#L91
[^code-brut-noyau]: Correspond à `KEY_Q` dans le fichier d’en-tête [`input-event-code.h`][input-event-codes.h].
[^code-symbolique-iso-9995]: Les codes symboliques sont suivent la norme [ISO/IEC 9995-2] pour les touches alpha-numériques.

Keysym

: Code numérique identifiant un symbole sur le _capuchon_ d’une touche. Ce mot
vient de l’anglais « key symbol ». Les keysyms sont également associées à des
noms anglais pour faciliter leur utilisation. Exemples : `a`, `agrave` pour
« à », `Shift_L` pour la touche majuscule à gauche, etc.
À la différence des keycodes, les keysyms ne sont pas utilisés pour _identifier_
les touches physiques mais pour configurer le _résultat_ obtenu en pressant une
touche. Ainsi, la _touche_ `<Q>` d’un clavier imprimé QWERTY peut être configurée
pour produire la keysym `q` ou `a` sur la couche de base, et les keysyms `Q` ou
`A` sur la couche masjcule, etc.

: Il existe différents types de keysyms :
  - _caractère :_ `a` et `A` pour les scripts latins, `gamma` « γ » et `GAMMA`
    « Γ » pour le grec, etc.
  - _touche morte :_ `dead_grave` et `dead_diaeresis`, qui correspondent respectivement
    à l’accent grave et au tréma. Une touche morte est une touche spéciale car elle ne
    génère pas de caractère, mais modifie le caractère de la touche qui est utilisée
    directement après elle. Ce comportement nécessite la fonctionnalité « Compose ».
  - _modificateur :_ une touche qui modifie l’effet des autres touches : par exemple
    `Shift_L`, `Control_R`, `Caps_Lock`. Les modificateurs utilisent un mécanisme
    différent des touches mortes et servent à accéder aux différentes couches d’une
    disposition, ainsi qu’à définir des raccourcis clavier.
  - _système :_ actions spéciales non comprises ci-dessus : flèche `Left`,
    `Pause`, `Escape`, `F1`, etc.

Key type

: TODO

Key Action

: TODO

Layout

: TODO

Keymap

: TODO