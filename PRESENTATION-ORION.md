# ORION — présentation du projet

*Texte prêt à publier : page GitHub, forum, Reddit, réseaux sociaux.*

---

## En une phrase

**ORION est un launcher de jeux PC gratuit qui détecte tous vos jeux, où
qu'ils soient, et les lance avec les réglages graphiques calculés pour votre
machine et pour ce que vous voulez en faire.**

---

## Pourquoi il existe

Un joueur PC a aujourd'hui Steam, Epic, GOG, Ubisoft Connect, l'EA app,
Battle.net, le Microsoft Store — et quelques jeux posés à la main dans un
dossier. Sept bibliothèques, sept interfaces, aucune vue d'ensemble.

Et à chaque nouveau jeu, le même rituel : entrer dans les options, deviner ce
que coûte chaque curseur, chercher un guide de réglages sur Internet, tester,
recommencer. Pendant ce temps, l'écran 180 Hz tourne à 60, la définition
n'est pas la bonne, et la carte graphique n'utilise pas la moitié de ce
qu'elle sait faire.

ORION est né de cette frustration. Il ne remplace pas Steam : il se place
au-dessus de tout, et s'occupe de ce que personne ne fait.

---

## Ce qu'il fait

**Il trouve vos jeux.** Neuf sources explorées : les manifestes Steam de
toutes vos bibliothèques, les manifestes Epic, la base de registre GOG,
Ubisoft, EA, Battle.net, les paquets Microsoft Store, vos dossiers de jeux
personnels, et un rattrapage prudent par la liste des programmes installés.
Les doublons sont fusionnés, les lanceurs écartés, les jeux dont les fichiers
ont disparu signalés.

**Il les habille.** Jaquettes, bannières et logos officiels, récupérés
automatiquement — y compris pour les jeux hors Steam, dont l'identifiant est
retrouvé à partir du titre. Un jeu sorti le jour même est reconnu.

**Il connaît votre machine.** Processeur, mémoire, stockage, carte graphique
avec ses capacités réelles (DLSS, génération d'images, ray tracing, Reflex,
FSR, XeSS), et tous vos écrans avec la totalité de leurs modes. Il sait même
faire la différence entre la définition native de votre dalle et les
super-résolutions du pilote.

**Il règle vos jeux.** Trois profils :

- **Esport** — latence minimale : détails réduits, post-traitement coupé,
  plein écran exclusif, limite d'images calée sous la fréquence de l'écran,
  Reflex actif. Les textures restent hautes, parce qu'elles coûtent de la
  mémoire vidéo et pas des images par seconde.
- **Détente** — l'équilibre : qualité élevée, super-résolution en mode
  qualité, fluidité stable au taux de rafraîchissement de l'écran.
- **Photoréaliste** — image maximale : ray tracing si la carte le permet,
  textures et distance d'affichage au plus haut, anticrénelage de qualité.

Les valeurs ne sont pas figées : elles sont **recalculées** à partir de votre
GPU, de sa mémoire vidéo, de votre processeur et de l'écran choisi. ORION
règle l'écran (définition et fréquence) puis écrit les options dans le jeu —
Unreal Engine, Unity, Source nativement, les autres via des recettes
partagées par la communauté.

**Il mesure vraiment.** Activée, la mesure enregistre les images par seconde
réellement affichées pendant la partie. ORION affiche ensuite moyenne, 1 %
bas et 0,1 % bas par profil, et propose des ajustements chiffrés : *« Détente
tourne à 72 i/s pour un écran à 180 Hz : baisser les ombres d'un cran et
passer la super-résolution en équilibré devrait rendre la fluidité. »* Le
profil s'adapte au fil des parties.

**Il surveille les prix.** Avis des joueurs, note Metacritic, prix actuel,
meilleure offre du moment sur des dizaines de boutiques, plus bas prix jamais
relevé, et un verdict clair : faut-il acheter maintenant ou attendre. Une
page « Envies » suit les jeux que vous n'avez pas encore, avec un seuil
d'alerte par jeu et une notification quand il est atteint.

**Il protège vos parties.** Détection des dossiers de sauvegarde, archivage
en zip horodaté lisible sans ORION, restauration qui met l'existant de côté
au lieu de l'écraser. Automatique après chaque partie et avant toute
désinstallation.

**Il fait le ménage.** Taille, dernière partie et temps de jeu croisés pour
montrer ce qui dort : *« 245 Go récupérables »*. ORION ne supprime jamais
rien lui-même — il archive la sauvegarde puis ouvre le désinstalleur de la
plateforme.

**Il se pilote à la manette.** Navigation complète au pad et affichage salon
plein écran, pour jouer depuis le canapé.

---

## Ce qu'il ne fait pas

Pas de publicité. Pas de compte à créer. Pas de télémétrie. Pas
d'abonnement. Pas de fonction bridée derrière un paiement. Pas de service
tiers installé dans votre dos.

Et surtout : **il n'écrit jamais dans un jeu sans montrer d'abord ce qui va
changer, demander confirmation, et sauvegarder les fichiers concernés.** Le
bouton « Restaurer » remet l'état précédent en un clic.

---

## Une IA, mais optionnelle

ORION fonctionne entièrement sans IA. Si vous collez une clé — Claude,
ChatGPT, Gemini, Mistral, ou **Ollama en local, sans clé ni connexion** —
quatre actions s'ajoutent, dont une qui change tout :

**« Apprendre ce jeu à ORION »** : l'IA lit les fichiers de configuration
réellement présents sur votre disque et écrit la recette qui permettra de
régler ce jeu automatiquement. Un jeu à moteur maison, que personne ne sait
configurer, devient réglable — et la recette peut être partagée avec tout le
monde.

La clé est la vôtre, l'IA ne coûte donc rien au projet. Avec Ollama, rien ne
quitte votre machine.

---

## Comment c'est fait

**ORION a été intégralement développé en *vibe coding*** : pas une ligne
tapée à la main. L'application est née d'une conversation en français avec
**Claude** (Anthropic), qui a conçu l'architecture, écrit les 12 000 lignes
de code, testé, corrigé les bugs sur la machine cible et livré le résultat.

Les outils et technologies employés :

| Domaine | Choix |
|---|---|
| Langage | **Python 3.13** |
| Interface | **PySide6 / Qt 6** — thème sombre entièrement personnalisé |
| API Windows | **ctypes** en direct : `user32` (écrans, changement de mode), `kernel32` (mémoire), **XInput** (manette), `winreg` (base de registre) |
| Réseau | **requests** |
| Processus | **psutil** |
| Données de jeux | API publiques Steam (fiche, avis, actualités, recherche), catalogue GOG, IsThereAnyDeal *(clé gratuite, facultative)*, SteamGridDB *(facultatif)* |
| Mesure des performances | **PresentMon** (Intel), téléchargé automatiquement |
| IA facultative | Claude, ChatGPT, Gemini, Mistral, Ollama |
| Développement | **Claude Opus 5**, en vibe coding, avec prise en main directe du PC de test |

L'architecture est modulaire de bout en bout : un registre de plugins
découvre automatiquement les sources de jeux, les fournisseurs de jaquettes,
les comparateurs de prix et les formats de réglages. Ajouter une plateforme,
c'est déposer un fichier Python. Apprendre un jeu, c'est déposer un fichier
JSON. Rien à recompiler, rien à modifier dans le code livré.

---

## Installation

1. Téléchargez et décompressez ORION.
2. Double-cliquez sur **`Installer.bat`** — il crée un environnement Python
   isolé et installe les dépendances.
3. Lancez **`ORION.bat`** ou le raccourci du Bureau.

Tout vit dans `%LOCALAPPDATA%\ORION` : configuration, bibliothèque, cache,
sauvegardes, journaux. Rien ailleurs.

---

## Soutenir le projet

ORION est gratuit et le restera. Si l'application vous rend service, un don
libre aide à la faire vivre : le bouton **Soutenir ORION** dans la barre
latérale ouvre la page de don.

---

<div align="center">

**ORION — vos jeux, votre matériel, les bons réglages. Sans y penser.**

</div>
