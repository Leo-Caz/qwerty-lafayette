+++
title = "Analyse et optimisation"
date = 2024-10-20T18:01:23+01:00
author = "kaze"
tags = ["communauté", "technique", "outils"]
+++

<!--
Étant mondialement connu pour mon objectivité totale, on me demande souvent des
trucs (et c’est bien normal). Notamment pour des questions liées aux claviers.

— C’est vrai qu’Ergo‑L est meilleur que Dvorak en anglais ?
— Totalement. En même temps, Dvorak date des années 1930, hein.
— Et meilleur que Bépo en français aussi ?
— Reste poli. Tu nous prends pour qui ?
— J’ai vu une variante de Bépo qui dit qu’elle est mieux.
— Haha, c’est mignon ça ! Mais non.
-->

Pour que chacun·e puisse comprendre en quoi Ergo‑L se distingue et quels sont
ses avantages et inconvénients par rapport aux autres dispositions de clavier,
il était grand temps d’écrire un article sur l’art délicat de l’analyse et de
l’optimisation des layouts.

<!--more-->

<style>
blockquote { background-color: var(--bg-banner); }
blockquote p { margin: 0.25em 0; }
.highlight,
blockquote,
blockquote + p { margin: 0.5em auto; max-width: 42em; box-sizing: border-box; }
blockquote + p { text-align: right; }
li li a[href] { color: var(--fg-main); }
code { font-family: monospace; }
</style>

:::{.highlight style="max-width: 32em;"}
- [Les fondamentaux]
  - [la heatmap]
  - [la charge des doigts]
  - [les digrammes]
  - [les trigrammes]
- [Critères d’évaluation]
  - [métriques indispensables]
  - [SHU, <i lang="en">same hand usage</i> ?]
  - [distance parcourue ?]
  - [note globale ?]
- [Optimiser pour une note globale ?]
  - [l’approche CarpalX]
  - [l’approche Optimot]
  - [une autre note globale est-elle possible ?]
- [Optimiser façon Ergonaute !]
  - [l’état de l’art]
  - [la méthode]
  - [les outils]
  - [la communauté]
- [Les principaux analyseurs]
  - [CarpalX]
  - [KLA (<i lang="en">keyboard layout analyzer</i>)]
  - [Colemak-DH]
  - [Oxeylyzer ❤️]
  - [Kalamine 🚀]
- [Conclusion]
:::


Les fondamentaux
--------------------------------------------------------------------------------

Quelles sont les principales caractéristiques d’une bonne disposition de clavier ?

### La heatmap

L’optimisation la plus évidente pour une disposition de clavier consiste à
placer les touches les plus fréquemment utilisées aux meilleurs emplacements :

- sur les 8 positions de repos
  <br>([A]{.kbd}[S]{.kbd}[D]{.kbd}[F]{.kbd} et [J]{.kbd}[K]{.kbd}[L]{.kbd}[;]{.kbd} en Qwerty) ;
- sur les 4 positions des majeurs et annulaires de la rangée supérieure
  <br>([W]{.kbd}[E]{.kbd} et [I]{.kbd}[O]{.kbd} en Qwerty) ;
- sur les 2 positions des index de la rangée inférieure
  <br>([V]{.kbd} et [M]{.kbd} en Qwerty).

Ces positions correspondent à celles notées 1 à 2 par le projet
[Workman](https://workmanlayout.org/#back-to-the-drawing-board).

![Accessibilité des touches selon Workman.](workman_grid.png)

On notera au passage que la question de l’accessibilité hors du pavé central de
3×10 touches ne s’est jamais posée chez Workman : le principe [1DFH][] va de soi
pour les dispositions anglophones.

### La charge des doigts

Une autre optimisation de base consiste à équilibrer la charge de travail des
doigts :

- les doigts forts (index, majeur) peuvent supporter plus de charge que les
  auriculaires, qui sont déjà très sollicités avec [Entrée]{.kbd},
  [Backspace]{.kbd}, [Tab]{.kbd}, [Shift]{.kbd}…
- la charge est aggravée par les extensions, i.e. les touches qui sont notées 3
  ou plus par le projet Workman (V. ci-dessus).

On affiche en bleu la charge liée aux touches notées 1 à 2, en jaune celle des
touches notées 3, et en orange celles notées 4 ou plus — ce qui inclut les
touches trop excentrées pour être évaluées par Workman, et qui enfreignent le
principe [1DFH][], auquel nous autres Ergonautes sommes si attaché·e·s.

![Charge des doigts d’Ergo‑L.](ergol.png)

![Charge des doigts de Bépo.](bepo.png)

### Les digrammes

Un digramme est un enchainement de deux touches.
Tout digramme appartient à l’une des catégories suivantes :

- alternance de mains : les touches sont sous deux mains différentes ;
- digramme de même doigt (SFB) : deux touches différentes à enchainer avec le
  même doigt ;
- répétition (SKB) : la même touche est pressée deux fois de suite.
- digramme de même main (SHB) : les touches sont sous deux doigts différents
  d’une même main.

On affiche les SKB en jaune et les SFB (plus gênants) en rouge. Le nombre de SFB
et SKB dépend fortement de la disposition de clavier, alors que le nombre de SKB
dépend essentiellement du corpus utilisé — mais l’utilisation d’une touche morte
est de nature à augmenter le nombre de SKB. On ne peut jamais annuler ces SFB et
SKB, mais on fait en sorte de les placer préférentiellement sur les doigts
forts, en évitant tout particulièrement les auriculaires.

![Répartition des SFB et SKB d’Ergo‑L.](ergol_sfu.png)

![Répartition des SFB et SKB de Bépo.](bepo_sfu.png)

Lors d’un enchainement rapide de deux touches, il est fréquent (voire
systématique) que la deuxième touche soit pressée avant que la première ne soit
relâchée. C’est particulièrement vrai pour les digrammes de même main.

Les digrammes de même main sont plus délicats à qualifier. On distingue :

- roulement intérieur : l’enchainement se fait confortablement de l’auriculaire
  vers l’index (le meilleur enchainement qui soit) ;
- roulement extérieur : l’enchainement se fait confortablement de l’index vers
  l’auriculaire (confort comparable à une alternance de mains) ;
- ciseau : l’enchainement requiert un changement de rangée inconfortable, comme
  [C]{.kbd}[R]{.kbd} en Azerty ou Qwerty ;
- extension (LSB, <i lang="en">lateral stretch bigrams</i>) : l’enchainement
  inclut une touche d’une colonne excentrée ou de la rangée des chiffres.

Le taux de SFB (ou SFU, pour <i lang="en">same finger usage</i>) est le
principal indicateur du niveau d’optimisation d’une disposition de clavier, et
on peut être tenté de l’utiliser comme indicateur principal de la qualité d’une
disposition de clavier. Mais attention, un SFU très bas cache parfois des
défauts rédhibitoires ailleurs — notamment sur les ciseaux, les extensions, ou
la charge des doigts.

### Les trigrammes

Un trigramme est un enchainement de trois touches.

Les critères « alternance », « roulement », « du même doigt » s’appliquent
toujours, mais on ajoute encore la notion de redirection pour les trigrammes
faits d’une même main avec un changement de direction, comme
[D]{.kbd}[S]{.kbd}[F]{.kbd} ou [K]{.kbd}[J]{.kbd}[L]{.kbd} en Azerty ou Qwerty.

La redirection est qualifiée de « mauvaise » quand elle ne fait pas intervenir
l’index.


Critères d’évaluation
--------------------------------------------------------------------------------

### Métriques indispensables

Un analyseur de disposition de clavier va, en tout premier lieu, fournir des
métriques sur les principaux critères :

:::{.highlight}
- la heatmap doit être centrée sur les positions confortables ;
- la charge des doigts doit être bien répartie et épargner les auriculaires ;
- le taux de digrammes de même doigt (SFU) doit être le plus bas possible ;
- le nombre de ciseaux et d’extensions (LSB) doit être le plus bas possible ;
- le taux de mauvaises redirections doit être le plus bas possible.
:::

Et **chacune de ces métriques est importante** : chez les Ergonautes, on
considère que la qualité ressentie d’une disposition est reflétée par sa pire
métrique parmi celles-ci, bien plus que par une moyenne (fût-elle pondérée) de
toutes ces métriques.

Les quatre premières métriques sont très consensuelles ; la dernière est moins
souvent prise en considération, mais de notre point de vue c’est une grosse
erreur que de la négliger.

### SHU, <i lang="en">same hand usage</i> ?

Le SHU mesure la répartition entre alternances de mains et roulements.

À l’époque des machines à écrire mécaniques, le SHU devait être le plus bas
possible car les roulements coinçaient souvent les marteaux : Qwerty, et encore
plus Dvorak, ont été développés dans cet objectif. C’est aussi le cas de Bépo et
de ses nombreuses variantes.

Mais, de nos jours, les claviers informatiques n’ayant pas de contrainte de ce
type, cette métrique du SHU n’est plus utilisée pour mesurer la qualité d’une
disposition — voire, elle est souvent utilisée dans l’autre sens : un SHU élevé
caractérise une disposition « rolly », c’est-à-dire privilégiant les roulements.
C’est le cas de la très grande majorité des dispositions modernes, dont Workman
et Ergo‑L.

> In designing Workman, I preferred a high SHU (low alternation) over a low SHU
> (high alternation). I think high alternation is beneficial if you’re typing on
> mechanical typewriters but not necessarily on modern keyboards. […]

> It is much more efficient to ride the momentum of a single arm or wrist stroke
> and type a combo rather than just one key.

— [Kevin DeLoach][kdeloach], disposition [Workman][]

C’est un constat qui est également partagé par bon nombre de Bépoètes.

> La frappe d’un roulement facile peut être plus rapide, plus confortable et
> moins sujette à la faute de frappe qu’une alternance de mains.

— extrait des notes de conception de [Béop][]

Et c’est un sujet qui a été longuement détaillé par [Nuclear-Squid][] dans sa
conférence « [Ergonomie clavier : l’ère post-Dvorak][cdl2023-slides] »
([vidéo][cdl2023-video]).

Attention : les dispositions de clavier qui privilégient les roulements prennent
le risque d’avoir un taux élevé de mauvaises redirections.
 
### Distance parcourue ?

Une métrique originale consiste à mesurer la distance parcourue par les doigts
pendant la saisie d’un texte. Elle a été rendue populaire par CarpalX et KLA :
facile à calculer, et c’est toujours amusant de savoir combien de kilomètres nos
doigts parcourent pour saisir un texte. :-)

La communauté Ergonaute n’utilise pas cette métrique car elle n’est pertinente
que si l’on suppose que tous les déplacements de doigt se valent — ce qui est
évidemment faux (voir le paragraphe sur la [heatmap](#la-heatmap)).

### Note globale ?

Certains analyseurs de layout proposent une note globale, qui est une moyenne
pondérée de plusieurs critères plus objectifs. Si vous connaissez les critères
utilisés et êtes d’accord avec leur pondération, cette note globale peut donner
une évaluation générale appréciable lors des premières phases d’optimisation.

Mais il y a deux choses importantes à garder à l’esprit :

- une note globale ne rend pas compte des pires défauts de la disposition : ils
  sont soit noyés dans la moyenne, soit complètement ignorés ;
- quelle que soit sa qualité, une note globale ne sera jamais une bonne cible
  d’optimisation.

> Lorsqu'une métrique devient un objectif, elle cesse d'être une bonne métrique.

— [loi de Goodhart](https://fr.wikipedia.org/wiki/Loi_de_Goodhart)


Optimiser pour une note globale ?
--------------------------------------------------------------------------------

Ça peut être contre-intuitif, mais optimiser pour une note globale est voué à
l’échec : chercher à atteindre la meilleure valeur va nécessairement dégrader
les métriques qui ne sont pas (ou pas suffisamment) prises en compte par la note
globale.

Pour s’en convaincre, il y a deux exemples assez caricaturaux : CarpalX et
Optimot.

### L’approche CarpalX

S’il existait une note globale pertinente, n’importe quel développeur aurait pu
déterminer une disposition de clavier optimale pour un corpus donné en
appliquant un algorithme de [recuit simulé][].

C’est ce qu’a fait [CarpalX][], qui est le projet le plus ancien et le plus
connu dans le domaine. Sa note globale est un [score d’effort][CarpalX-effort]
qui est basé sur un modèle assez complexe prenant en compte de multiples
critères, notamment :

- l’alternance des mains ;
- le SFU ;
- les roulements ;
- la réduction de la charge des auriculaires ;
- la limitation des enchainements complexes.

CarpalX a ainsi abouti à la disposition [QFMLWY][], qui a le meilleur score
d’effort possible. Et la disposition [Qwerty-Flip][] a un score d’effort quasi
identique à Dvorak, alors qu’elle est très proche de Qwerty — et donc bien plus
simple à apprendre, tout en conservant les raccourcis clavier usuels.

![Qwerty-Flip (illustration du site de l’auteur).](qwerty-flip.gif)

Et pourtant, personne n’utilise ces dispositions. Pourquoi ?

- soit c’est un simple manque de notoriété : elles sont très bonnes mais trop
  peu connues ;
- soit le score d’effort est une métrique imparfaite, et un très bon score
  d’effort peut masquer des défauts majeurs.

Et de fait : le score d’effort accorde bien trop peu d’importance au SFU. Il
s’élève à 4,6 % pour QFMLWY, bien loin de Dvorak (2,7 %), Colemak (1,6 %) ou
Ergo‑L (1,2 %). Quant à Qwerty-Flip, son SFU est très logiquement le même que
celui de Qwerty, soit 5.7 %. Le résultat est constatable immédiatement, et ce
n’est là que le principal défaut de ces dispositions.

> The CarpalX layout seemed attractive due to its supposed scientific derivation.
> After getting up to 10 WPM, I think I preferred it to Dvorak. It seemed to
> have surprisingly high same finger usage — especially the right index.

> Digrams using A, F, I, and P felt uncomfortable, and common enough to really
> bug me. Seemed like a big oversight to an otherwise great layout.

— [u/fullyassociative]

La démarche de CarpalX est basée sur un [modèle d’effort][CarpalX-effort] très
précis, qui donne l’illusion qu’optimiser pour ce score d’effort aboutira de
façon scientique à la meilleure disposition possible ; et, intuitivement, on a
envie d’y croire !

Mais, en pratique, toutes les dispositions issues de ce type d’optimisation ont
des défauts rédhibitoires qui sont noyés dans la moyenne du score d’effort. Ce
score, aussi élaboré soit-il, ne parvient pas à rendre compte de la qualité
d’une disposition.

À l’usage, on a constaté que CarpalX trouvait rapidement des dispositions
correctes avec un SFU pas trop élevé et une bonne répartition de la charge des
doigts, puis qu’à chaque itération il proposait des dispositions marginalement
meilleures pour le score d’effort mais où le SFU se dégradait fortement. On
atteint là les limites de l’optimisation mono-critère.

### L’approche Optimot

S’il existait une note globale pertinente mais que vous n’aviez pas de
compétence en programmation, vous pourriez passer par un analyseur en ligne qui
propose ce type d’évaluation et, à force d’essais, vous obtiendriez une
disposition très bien notée pour votre langue cible — probablement le français,
si vous lisez cet article.

C’est l’approche retenue par Optimot, une variante non libre de Bépo.
Étonnamment, l’analyseur retenu est [KLAnext][], qui est [loin d’être le plus
abouti][les principaux analyseurs]. Ayant optimisé sa disposition pour KLAnext,
l’auteur d’Optimot affirme ainsi que sa disposition est la meilleure en
français, puisque c’est celle qui a la meilleure note sur KLAnext.

Faisons abstraction du raisonnement circulaire et intéressons-nous à l’anglais :
dans cette langue, Optimot a une note KLAnext quasi équivalente à celle de Colemak
et MTGAP, qui sont deux des meilleures dispositions anglophones modernes.
Comment est-ce possible ? Alors que c’est un domaine de recherche très actif
chez les anglo-saxons depuis deux décennies ? Et alors qu’Optimot dédie beaucoup
de bonnes touches aux lettres accentuées du français ? Et alors que son auteur
confirme que l’anglais n’est qu’un objectif secondaire de cette disposition ?

> Moi aussi, je peux modifier légèrement Optimot pour optimiser un peu plus pour
> l’anglais (mais au détriment du français). Mais ce n’est pas mon choix parce
> que nous sommes en France et que je m’adresse à des personnes qui écrivent
> d’abord en français.

— Pyjam, auteur d’Optimot

Là encore, deux hypothèses sont envisageables :

- soit l’auteur d’Optimot a un esprit supérieur comme le monde n’en connait que
  rarement ;
- soit il a mis en évidence une faille de la note globale KLAnext.

Fatalement, la deuxième hypothèse est de loin la plus probable. Et de fait, la
note globale de KLAnext comporte des failles évidentes.

- Elle *pénalise* les roulements, qui sont pourtant les meilleurs enchainements
  possibles sur un clavier informatique. Optimiser pour KLAnext suppose donc de
  *casser* les roulements et ainsi de *dégrader* la disposition.
- Elle ne pénalise ni les extensions de doigts, ni les ciseaux : le `EN`
  d’Ergo‑L et le `WH` de Bépo (<kbd>D</kbd><kbd>F</kbd> et
  <kbd>]</kbd><kbd>.</kbd> en Qwerty) ont la même pénalité, alors qu’il s’agit
  respectivement du meilleur et du pire enchainement possible. Optimiser pour
  KLAnext fait privilégier les *ciseaux* aux roulements.
- Elle ne semble pas prendre en compte l’équilibre de la charge des doigts.
  Optimot a une charge de plus de 11 % sur l’auriculaire droit en français, ce
  qui est exceptionnellement élevé pour une disposition de clavier (ergonomique
  ou non) et rédhibitoire pour nombre d’utilisateurices.
- Elle est plus sensible à la géométrie du clavier qu’à la disposition des
  touches. Ainsi, pour l’anglais, Bépo sur Ergodox a une meilleure note que
  Sturdy sur ANSI — s’agissant là respectivement de la pire et de la meilleure
  disposition qui soient pour cette langue, cette note ne traduit pas du tout
  l’écart de confort ressenti.

![Scores KLAnext de Bépo et Sturdy en anglais.](klanext_bepo.png)

Le cas de KLAnext est un peu caricatural, mais à mon sens le problème ne vient
pas tant de l’analyseur que du mésusage de sa note globale : elle peut donner
une première appréciation générale, mais elle n’est pas une bonne cible
d’optimisation.

Tout ceci n’invalide pas les qualités d’Optimot : comme on le dit dans notre
[comparateur][], cette disposition reste une belle amélioration de Bépo pour le
même objectif, écrire en français sur un clavier standard. Mais elle n’est [pas
optimisée pour l’anglais][optimot-en], comme le reconnait son auteur à juste
titre ; et, si l’optimisation basée sur KLAnext a permis de réduire
significativement le SFU, elle n’a pas permis de corriger le nombre de ciseaux
(LSB) et le mauvais équilibre de la charge des doigts, deux défauts hérités de
Bépo mais ignorés par KLAnext.

### Une autre note globale est-elle possible ?

Après avoir constaté que les notes globales de CarpalX et KLA/KLAnext étaient
mauvaises, j’ai longtemps été persuadé qu’il devait *forcément* y avoir une
bonne métrique globale ailleurs.

Mais, à l’usage, on s’est rendu compte que toute note globale présentera les
mêmes défauts :

- c’est une notation très subjective, puisque la pondération des différents
  critères change complètement le résultat ;
- ça n’est pas une bonne cible d’optimisation, car cela pousse à négliger les
  défauts peu punis par la notation ;
- ça n’est pas un bon critère d’évaluation non plus, une disposition pouvant
  avoir un défaut rédhibitoire sans que cela affecte la note globale.

Durant la conception d’Ergo‑L, on a perdu beaucoup de temps sur le projet à
tenter des optimisations mono-critères avec un [algorithme génétique][] ou de
[recuit simulé][]. Certains outils plus aboutis comme <i lang="en">[Keyboard
Layout Optimizer][KLO]</i>, qui a été utilisé pour Neo2, nous semblaient
prometteurs ; mais, à l’usage, ils ont été bien moins utiles que de simples
boucles pour explorer des possibilités par force brute, que [Nuclear-Squid][] a
codées vite fait.

> Les chiffres sont aux analystes ce que les lampadaires sont aux ivrognes :
> ils fournissent bien plus un appui qu’un éclairage.

— Jean Dion

C’est un gros <i lang="en">red flag</i> quand une disposition met en avant une
note globale plutôt que des métriques objectives, car c’est souvent une façon
(délibérée ou non) de passer sous silence les pires aspects d’une disposition de
clavier. Et ça devient franchement trompeur quand la disposition a été optimisée
pour cette note globale.


Optimiser façon Ergonaute !
--------------------------------------------------------------------------------

Comme on vient de le voir, ce n’est pas tant l’analyseur que son utilisation qui
est en cause : vouloir évaluer ou optimiser des dispositions à l’aune d’une note
globale est voué à l’échec. Il faut procéder autrement.

### L’état de l’art

Avant de se lancer dans l’élaboration d’une disposition de clavier, il est
vivement recommandé de chercher un maximum d’informations sur le sujet. Les
mille et une variantes de Bépo qui ont fleuri laissent penser que la plupart des
adeptes francophones d’ergonomie clavier sont restés sur les principes Dvorak
qui, datant des années 1930, concernaient les machines à écrire.

Or, beaucoup de choses ont changé depuis une petite vingtaine d’années, avec
notamment : 

- des dispositions de clavier basées non plus sur l’alternance de mains, mais
  sur les roulements — Colemak a ouvert la voie, suivie de bien d’autres ;
- les [claviers compacts][] et l’approche [1DFH][], qui réduisent drastiquement
  les mouvements de doigts ;
- des analyseurs qui, utilisés avec soin, permettent de sortir de l’évaluation
  « au doigt mouillé ».

On essaye de regrouper et vulgariser un maximum d’informations à ce sujet sur ce
site et sur le [serveur Discord][], en espérant que ça puisse aider les auteurs
et autrices de disposition. Côté anglophone, [r/KeyboardLayouts][] et le
[Keyboard Layouts doc][] sont des mines d’or.

### La méthode

> Quelle que soit la disposition de clavier, son pire défaut se ressentira
> toujours plus que ses meilleures qualités.

— crédo ergonaute

> Soyez pas cons : ayez des stats.

— [Ergonomie clavier : l’ère post-Dvorak](https://www.youtube.com/watch?v=96RikfmBY-U&t=2017s)

C’est l’approche que l’on propose sur notre [comparateur][] et qu’on a suivie
pendant toute la mise au point d’Ergo‑L. On a itéré comme suit :

1. Identifier le pire achoppement de la disposition (SFB, ciseau, redirection…).
2. Améliorer notre analyseur pour qualifier et mesurer cet achoppement.
3. Trouver une modification du layout qui, sur la foi de l’analyseur, réduise
   cet achoppement.
4. Utiliser ce layout jusqu’à détecter un autre achoppement (généralement moins
   grave).
5. `GOTO 1`.

On n’a donc jamais eu aucun usage d’une note globale. Au contraire, on regarde
toujours la pire note et les pires enchainements pour évaluer une disposition et
proposer des améliorations.

Cela dit, il y a bien une métrique que l’on regarde plus que les autres, c’est
le SFU : ça donne assez rapidement une idée de la marge d’optimisation, qui
reste possible. Pour autant, et même si on est très fièr·e·s du SFU d’Ergo‑L en
français comme en anglais, ça n’est pas un objectif en soi : [Nuclear-Squid][] a
même rejeté des versions de développement d’Ergo‑L qui avaient des SFU
incroyablement bas, mais qui causaient d’autres problèmes plus sournois à
l’usage.
 
C’est notamment le cas de [Colemak French Touch][], sur lequel on est tombé un
peu accidentellement sur la fin du projet. Le SFU est terrifiant (0.7 %),  le
fait de coller à une disposition très connue était un avantage auquel on était
sensible, à tel point qu’on a envisagé d’annuler la sortie (alors imminente)
d’Ergo‑L 1.0 ! Mais deux problèmes sont apparus assez vite :

- la charge des doigts était trop déséquilibrée, surtout en anglais
  étrangement ;
- la redirection `OUI` était *très* inconfortable. Et on est retombé sur une
  conclusion qui nous était déjà apparue plus tôt dans le projet : soit on
  répartit ces trois lettres sur les deux mains, soit il faut que l’une des
  trois soit sous un index.

On constate que les enchainements inconfortables évoluent de deux façons
possibles avec la pratique : soit ils deviennent acceptables, soient ils se
révèlent insupportables. D’où l’intérêt de pratiquer la disposition qu’on
utilise – et idéalement, d’être plusieurs personnes différentes à pratiquer.
Les zones d’inconfort sont propres à chacun·e d’entre nous, et cela peut
dépendre autant de la personne que du type de clavier.

En ce qui me concerne, mes premiers tests d’Ergo‑L remontent à la version 0.7,
qui ne diffère que très légèrement d’Ergo‑L 1.0. Et bien qu’Ergo‑L 0.7 ait des
métriques excellentes, le digramme `if` (<kbd>L</kbd><kbd>P</kbd> en Azerty ou
Qwerty) m’était très inconfortable. Ergo‑L avait beau être meilleur que
Lafayette *dans l’ensemble*, le fait qu’il soit pire sur un point aussi
désagréable me dissuadait totalement de changer de disposition. Le problème a
été résolu par [Moussx][] avec une permutation de trois touches : ça peut
paraitre anecdotique, mais ça a *complètement* changé mon expérience de cette
disposition de clavier.

Il faut évidemment avoir des stats solides, et savoir les faire évoluer tout au
long de l’optimisation d’une disposition de clavier ; mais il nous semble tout
aussi essentiel d’alterner entre des phases d’optimisation et des phases
d’expérimentation pour mettre en lumière les enchainements inconfortables. Et ne
jamais perdre de vue que ce sont ces enchainements, plus que les métriques, qui
font la qualité d’une disposition de clavier.

### Les outils

Les itérations de développement ont été facilitées par :

- [x‑keyboard][], pour tester nos layouts ;
- [kalamine][], pour générer et installer les pilotes ;
- [notre analyseur maison](/stats).

On a développé notre propre analyseur pour plusieurs raisons :

- aucun analyseur existant ne prenait en compte les touches mortes, alors que
  toutes les dispositions francophones en font usage — et c’est même un élément
  fondamental d’Ergo‑L ;
- on a voulu mettre en lumière certains défauts de la disposition au fur et à
  mesure de l’avancement du projet, et qui n’étaient pas toujours pris en compte
  par les autres analyseurs : part des extensions dans la charge des doigts,
  qualification des redirections, repérage des ciseaux…
- x‑keyboard, qui avait été développé bien plus tôt, avait déjà beaucoup des
  fonctionnalités requises pour développer un analyseur ;
- c’était simple et fun à faire. :-)

Bien évidemment, on a vérifié que, pour un même layout et un même corpus, notre
analyseur donnait les mêmes résultats que les analyseurs existants. Et, bien
sûr, tout est disponible sous licence libre pour que chacun·e puisse étudier,
modifier, utiliser et rediffuser le tout comme bon lui semblera.

Outre les métriques, cet analyseur a pour but de lister tous les digrammes et
trigrammes qui peuvent causer de l’inconfort. Ce n’est pas tant un <i
lang="en">benchmark</i> qu’un outil d’optimisation.

### La communauté

Faire une disposition de clavier pour soi-même est relativement aisé ; en faire
une qui convienne au plus grand nombre, c’est une autre histoire.

En particulier, on a tou·te·s des niveaux de tolérance différents à certains
défauts de layout : pour moi les extensions d’auriculaires sont particulièrement
pénibles, alors que d’autres préfèrent ça plutôt que d’utiliser AltGr ;
certain·e·s s’accommodent bien des ciseaux (notamment les utilisateurices de
claviers 3D), d’autres pas du tout ; et les mauvaises redirections sont le point
le plus clivant : certain·e·s s’y font, mais beaucoup trouvent ça rédhibitoire à
l’usage.

Pour prendre en compte toutes ses particularités, notre analyseur ne se contente
pas de mesurer chaque type d’achoppement mais les détaille en listant tous les
digrammes et trigrammes pouvant poser problème. Ça nous a fait gagner beaucoup
de temps en facilitant les échanges de la communauté des Ergonautes pendant le
développement d’Ergo‑L.


Les principaux analyseurs
--------------------------------------------------------------------------------

Notre analyseur n’est ni le premier, ni le dernier à être développé. Petit tour
d’horizon des autres analyseurs parmi les plus connus et les plus utiles.

### CarpalX

[CarpalX][] est un analyseur et optimiseur en Perl, proposé par [Martin
Krzywinski][] sous licence non libre (CC-BY-NC-SA 4.0). Le [code
source][CarpalX-source] est disponible sur son site, la dernière modification
(version 0.12) remonte à 2015.

CarpalX a un intérêt historique mais, comme [mentionné plus
haut](#lapproche-carpalx), son score d’effort ne permet pas de fournir une
évaluation fiable. Loin s’en faut. Il a globalement été une perte de temps
pour le développement d’Ergo‑L.

### KLA (<i lang="en">Keyboard Layout Analyzer</i>)

[KLA][] est un analyseur libre en PHP et JS, proposé par [Patrick
Gillespie][patorjk] sous licence libre (MIT). Le [code source][KLA-source] est
disponible sur GitHub, la dernière modification remonte à 2019.

[KLAnext][] est un fork non libre de KLA par [Ian Douglas][]. Ce fork est
lui-même dérivé de [KLAtest][] ([source][KLAtest-source]) par [Xay Vong][],
a.k.a. Shena’Fu ou Den. Sans dépôt de code, difficile d’évaluer ce qu’apporte
KLAnext à l’original — mais, comme évoqué plus haut, il ne nous semble pas
pertinent. C’est en référence aux failles de KLAnext que la plaisanterie
« *[Qwerty-Lafayette est le meilleur layout du monde !][lafayette_mldm]* » est
devenue récurrente dans la communauté ergonaute. :-)

Plus intéressant, [SteveP][] a développé un [fork libre de KLA][KLA-SteveP]
([source][KLA-SteveP-source]) et détaille précisément les [corrections
apportées][KLA-SteveP-about] :

- le calcul de distance parcourue est remplacé par une évaluation de *pénalité*
  de distance, qui est pondérée par doigt pour prendre en compte la [loi de
  Fitts][] — ça n’est pas aussi poussé que ce que proposent Workman ou
  Colemak-DH, mais c’est déjà un progrès très significatif ;
- le SHU n’est plus du tout pris en compte dans le calcul de la note globale, si
  bien que les roulements ne sont plus considérés comme une pénalité. Enfin !

Chaque variante de KLA a ses propres paramètres de pondération pour la note
globale, qui est par nature très subjective. On recommande d’ignorer cette note.

Le fork de SteveP propose des métriques plus saines que KLAnext. À notre
connaissance, c’est la version de KLA la plus utilisée. C’est aussi la version
qui a été la mieux maintenue : son développement ne s’est arrêté qu’en mai 2021.

Toutefois, sur les [5 critères indispensables][métriques indispensables] à nos
yeux, seul le SFU est analysé par KLA. Attention à ne pas perdre de vue les 4
autres.

### Colemak-DH

[Colemak-DH][] est un projet qui a enthousiasmé beaucoup d’anglophones, à juste
titre : c’est une belle amélioration de Colemak, qui lui confère un beau
rééquilibrage de la charge des doigts, proche de celui de Workman (qui fait
office de référence dans ce domaine).

Et comme c’est un projet d’ampleur, ses contributeurs — dont un certain SteveP —
ont développé [un analyseur][Colemak-DH-analyzer] qui reflète les choix de cette
disposition, notamment la recherche de bons roulements et d’une bonne
répartition de la charge des doigts. Le [code source][Colemak-DH-source] (JS) de
cet analyseur est disponible sous licence libre (CC0).

C’est un analyseur plus complet que KLA, qu’il semble avoir remplacé — au moins
pour les développeurs qui y ont contribué. Le dernier commit remonte à juin
2022.

### Oxeylyzer ❤️

[Oxey][] est un auteur de dispositions de clavier très reconnu, notamment pour
[Sturdy][] qui est d’une efficacité redoutable en anglais : un SFU très bas
(0.9 %), beaucoup de roulements, très peu de ciseaux. Du grand art !

Oxey propose aussi un analyseur très complet avec son [layout playground][],
dont le [code source][oxeylyzer] (Rust) est disponible sous licence libre
(Apache 2.0). Cet « Oxeylyzer » est à nos yeux le meilleur analyseur du moment :

- des métriques précises, complètes et pertinentes : sa notion de  mauvaises
  redirections, notamment, nous a été très utile ;
- facile à interpréter grâce aux codes de couleur (vert, c’est bien ; rouge,
  c’est mal) ;
- pas de note globale (tant mieux !), mais efficace pour vite repérer les points
  faibles d’une disposition ;
- très pratique pour tester des permutations de touches.

Il est limité aux dispositions [1DFH][] (3×5 touches par main), ce qui nous
semble très pertinent d’un point de vue ergonomique, mais ça serait un
inconvénient pour des dispositions du type Bépo, qui font le choix d’étaler les
lettres sur deux colonnes supplémentaires afin de moins recourir aux touches
mortes.

Oxeylyzer est vraiment la référence pour nous. On le recommande vivement ! Et le
projet est activement maintenu, le dernier commit datant de moins de 6 mois à
l’heure où j’écris ces lignes.

### Kalamine 🚀

[Kalamine][] est avant tout le générateur de pilotes que l’on a développé pour
Qwerty-Lafayette et Ergo‑L ; mais, au fil du temps, il s’est transformé en outil
de mise au point tout-en-un pour les auteurs et autrices de dispositions de
clavier. L’analyseur d’Ergo‑L vient ainsi d’être intégré à Kalamine, ce qui
permet de visualiser directement l’impact de chaque modification de layout.

Le générateur est écrit en Python, l’analyseur en JavaScript, et le code source
est proposé sous licence libre (MIT).

Il n’est pas encore au niveau d’Oxeylyzer mais il a pour nous des avantages
importants, notamment :

- l’intégration de [x‑keyboard][] pour visualiser la disposition et tester
  rapidement une modification sans avoir à l’installer ;
- et surtout, le support des touches mortes ! À notre connaissance, c’est le
  seul analyseur qui dispose de cette fonctionnalité.

On espère qu’en mettant notre analyseur maison à disposition dans Kalamine il
pourra servir à d’autres projets qu’Ergo‑L et les dispositions de la famille
Lafayette. Et il est toujours en développement actif, notamment pour les projets
Erglace et Hypergol.


Conclusion
--------------------------------------------------------------------------------

- Il n’y a pas de mauvais analyseur, juste des mauvaises façons de s’en servir.
- Il n’y a pas de bonne note globale, ni de bonne façon de s’en servir.
- Chaque métrique est importante, car on a toutes et tous nos préférences et nos
  ressentis.

Et les [5 critères indispensables][métriques indispensables] à nos yeux sont les
suivants :

:::{.highlight}
- la heatmap doit être centrée sur les positions confortables ;
- la charge des doigts doit être bien répartie et épargner les auriculaires ;
- le taux de digrammes de même doigt (SFU) doit être le plus bas possible ;
- le nombre de ciseaux et d’extensions (LSB) doit être le plus bas possible ;
- le taux de mauvaises redirections doit être le plus bas possible.
:::

Un grand merci à [Nuclear-Squid][], non seulement pour avoir initié et dirigé le
projet Ergo‑L, mais plus prosaïquement pour sa contibution à la rédaction du
chapitre sur les analyseurs. Que le Grand Palmipède parsème son chemin de
pétales de roses.

Merci aussi à [Moussx][], [Meriem][], [aurelberra][], [Adrienm7][] et
[Xiloynaha][] pour la relecture, les suggestions et les corrections. C’est un
article que je n’aurais jamais pu écrire tout seul. La communauté Ergo‑L est
fantastique. :-)


[1DFH]:                    /presentation/#dfh-1u-distance-from-home
[Erglace]:                 /erglace
[Colemak French Touch]:    /lafayette/#colemak-french-touch
[claviers compacts]:       /claviers/compacts
[comparateur]:             /alternatives/#tableau-comparatif
[optimot-en]:              /alternatives/#bépo-et-ses-variantes
[adaptations]:             /claviers/#les-limitations-de-bépo-béopy-optimot
[cdl2023-slides]:          /slides/capitoledulibre2023
[cdl2023-video]:           https://www.youtube.com/watch?v=96RikfmBY-U

[x‑keyboard]:              https://github.com/OneDeadKey/x-keyboard
[kalamine]:                https://github.com/OneDeadKey/kalamine

[Qwerty-Lafayette]:        https://qwerty-lafayette.org
[lafayette_mldm]:          https://mastodon.social/@fabi1cazenave/111806300874072301
[Workman]:                 https://workmanlayout.org/#same-hand-utilization-shu
[Colemak-DH]:              https://colemakmods.github.io/mod-dh
[Colemak-DH-analyzer]:     https://colemakmods.github.io/mod-dh/analyze.html
[Colemak-DH-source]:       https://github.com/ColemakMods/mod-dh/tree/gh-pages
[Oxey]:                    https://oxey.dev
[Sturdy]:                  https://oxey.dev/sturdy
[layout playground]:       https://oxey.dev/playground/
[Oxeylyzer]:               https://github.com/O-X-E-Y/oxeylyzer
[Béop]:                    http://beop.free.fr/index.php/Main/Pourquoi#Roulements
[recuit simulé]:           https://fr.wikipedia.org/wiki/Recuit_simulé
[algorithme génétique]:    https://fr.wikipedia.org/wiki/Algorithme_génétique
[CarpalX]:                 https://mk.bcgsc.ca/carpalx/
[CarpalX-source]:          https://mk.bcgsc.ca/carpalx/?download_carpalx
[CarpalX-effort]:          https://mk.bcgsc.ca/carpalx/?typing_effort
[QFMLWY]:                  https://mk.bcgsc.ca/carpalx/?full_optimization
[Qwerty-Flip]:             https://nick-gravgaard.com/qwerty-flip
[KLA]:                     https://patorjk.com/keyboard-layout-analyzer
[KLA-source]:              https://github.com/patorjk/keyboard-layout-analyzer
[KLAnext]:                 https://klanext.keyboard-design.com
[KLAtest]:                 https://klatest.keyboard-design.com
[KLAtest-source]:          https://bitbucket.org/Shenafu/keyboard-layout-analyzer
[KLA-SteveP]:              https://stevep99.github.io/keyboard-layout-analyzer/
[KLA-SteveP-about]:        https://stevep99.github.io/keyboard-layout-analyzer/#/about
[KLA-SteveP-source]:       https://github.com/stevep99/keyboard-layout-analyzer
[loi de Fitts]:            https://fr.wikipedia.org/wiki/Loi_de_Fitts
[KLO]:                     https://github.com/dariogoetz/keyboard_layout_optimizer
[Keyboard Layouts doc]:    https://bit.ly/layout-doc-v2
[r/KeyboardLayouts]:       https://www.reddit.com/r/KeyboardLayouts/

[Nuclear-Squid]:           https://github.com/Nuclear-Squid
[Moussx]:                  https://github.com/gagbo
[Meriem]:                  https://mastodon.xyz/@meriem
[aurelberra]:              https://github.com/aurelberra
[kdeloach]:                https://github.com/kdeloach
[patorjk]:                 https://patorjk.com/
[SteveP]:                  https://github.com/stevep99
[Martin Krzywinski]:       https://mk.bcgsc.ca/
[Xay Vong]:                https://bitbucket.org/Shenafu
[Ian Douglas]:             https://github.com/iandoug
[u/fullyassociative]:      https://www.reddit.com/r/Colemak/comments/643uq4/tried_dvorak_carpalx_qgmlwy_and_now_colemak/