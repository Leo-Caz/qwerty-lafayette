+++
title = "Foire aux questions"
+++

**🚧 En construction 🚧**

<style>
h4 {
    font-size: 1.1rem;
}
</style>

Cette page apporte des réponses aux questions les plus fréquentes. N’hésitez pas
à nous rejoindre sur [le serveur Discord Ergo‑L](https://discord.gg/5xR5K3nAFX)
pour en savoir davantage !


Projet et site web
--------------------------------------------------------------------------------

#### Que veut dire \[…\] ?

Certains termes sont spécifiques à la création de dispositions clavier ou à la
typographie. Notre [glossaire] permet d’y voir plus clair.


#### D’où vient le nom « Ergo‑L » ?

Ergo‑L signifie « **Ergo**nomic **L**afayette », le projet ayant démarré comme
un fork de [QWERTY-Lafayette] visant à lui apporter une optimisation de type
Colemak/Workman. Il se prononce « ergol », comme le nom générique des carburants
de moteurs-fusées.

#### Pourquoi tous ces 🦆 ?

::: {.dialog}
- Coin coin ?
- Ook, ook. Ook !
:::

Pilotes
--------------------------------------------------------------------------------

### Linux

#### Ma disposition clavier ne fonctionne plus. Que faire ?

Si vous avez installé votre disposition avec [Xkalamine], cela peut arriver
après une mise à jour. Il vous suffit de la réinstaller avec [XKalamine]. Notez
qu’il existe d’[autres méthodes][xkb-custom] plus robustes.

#### La touche [★]{.odk} ne fonctionne pas. Que ce passe-t-il ?

Avec certains bureaux (Gnome notamment), la touche Typo [★]{.odk} ne fonctionne
que si Ergo‑L est défini comme diposition par défaut, c’est-à-dire en haut de
la liste des préférences claviers.

#### Pourquoi la touche [★]{.odk} fonctionne-t-elle en la maintenant pressée, alors que c’est une [touche morte] ?

Bien que la touche [★]{.odk} soit qualifiée de [touche morte], elle est
implémentée en utilisant un modificateur dit « _latch_ », qui s’utilise de deux
façons :

- soit en _relachant_ [★]{.odk} avant de taper la touche correspondant au
  caractère composé ;
- soit en _maintenant_ [★]{.odk} enfoncée en tapant cette touche.

Exemple pour Ergo‑L :

- [★]{.kbd} [A]{.kbd} → `à`
- [★]{.kbd} (maintien) [A]{.kbd} [★]{.kbd} (relâche) → `à`

#### J’utilise Wezterm et la touche [★]{.odk} imprimme un `o`. Que faire ?

C’est une [régression connue][wezterm-bug], [un patch est en
cours][wezterm-patch].


### Windows

#### Les touches mortes chainées ne marchent pas dans Firefox ?

Les touches mortes chainées ne sont malheureusement pas reconnues par certaines
applications, notamment [Firefox][firefox-cdk] et [Wezterm][wezterm-cdk].

#### La touche [AltGr]{.kbd} cause des problèmes dans certaines applis. Comment corriger ça ?

Comme [AltGr]{.kbd} est équivalent à [Ctrl]{.kbd}-[Alt]{.kbd} sous Windows, les
raccourcis clavier de certaines applications peuvent être déclenchés par
[AltGr]{.kbd}.

Avec GeForce Experience, [AltGr]{.kbd}-[M]{.kbd} (pour écrire `&`) peut être
capté par « Superposition en jeu » pour couper le micro.
Il suffit d’aller dans GeForce Experience sur la roue dentée > Généralités >
Superposition en jeu : Paramètres > Raccourcis claviers, pour changer ou
supprimer ce raccourci. Il est aussi possible de désactiver complètement la
Superposition en jeu.

De même avec Keepass 2, [AltGr]{.kbd}-[A]{.kbd} (pour écrire `{`) est capté même si
le programme n’est pas au premier plan. Pour cela, aller dans Tools > Options… >
onglet Integration > encart System-wide hot keys, et changer ou supprimer la
valeur du raccourci Global auto-type.



[glossaire]:        /glossaire
[touche morte]:     /glossaire#touche-morte-def
[QWERTY-Lafayette]: /lafayette/#qwerty-lafayette
[XKalamine]:        https://github.com/OneDeadKey/kalamine#xkalamine
[xkb-custom]:       https://github.com/OneDeadKey/kalamine#linux-root-xkb_symbols

[firefox-cdk]:       https://bugzilla.mozilla.org/show_bug.cgi?id=1910287
[wezterm-cdk]:       https://github.com/wez/wezterm/issues/5866
[wezterm-bug]:       https://github.com/wez/wezterm/commit/b8d93edce6267b09d8926f13de9620ad1ae5ea1f
[wezterm-patch]:     https://github.com/wez/wezterm/pull/4991
