<div align="center">

# ORION — Recettes communautaires

**La base de connaissances partagée du launcher ORION.**
Chaque recette apprend à l'application comment régler un jeu.

</div>

---

## C'est quoi ORION ?

Un launcher de jeux PC qui fait ce que les autres ne font pas : **il règle
les jeux à votre place**.

Il détecte tout ce qui est installé sur la machine — Steam, Epic, GOG,
Ubisoft, EA, Battle.net, Microsoft Store, et les jeux posés à la main dans un
dossier — récupère les jaquettes officielles, analyse le matériel et les
écrans, puis lance chaque jeu avec des réglages graphiques **calculés pour la
configuration réelle** et pour ce qu'on veut en faire : compétition, détente,
ou image maximale.

Gratuit, sans publicité, sans compte, sans télémétrie.

## Et ce dépôt, alors ?

ORION sait régler nativement les jeux Unreal Engine, Unity et Source. Pour
tous les autres — moteurs maison, jeux récents, cas particuliers — il a
besoin d'une **recette** : un petit fichier JSON qui lui dit où sont les
options du jeu et comment les écrire.

Une recette écrite par une personne sert à tout le monde. C'est le rôle de ce
dépôt : ORION lit `index.json` une fois par jour et télécharge les recettes
nouvelles ou mises à jour. Rien n'est envoyé depuis le poste de
l'utilisateur ; la synchronisation est en lecture seule.

## Proposer une recette

1. Dans ORION, ouvrez la fiche du jeu et cliquez sur **Partager cette
   recette** : deux fichiers sont créés dans votre dossier ORION.
2. Déposez `<id>.json` dans le dossier [`recipes/`](recipes/) de ce dépôt.
3. Ajoutez la ligne du fichier `<id>.index.json` dans
   [`index.json`](index.json).
4. Ouvrez une pull request.

Augmentez `version` d'une unité à chaque correction pour que la recette soit
redistribuée aux utilisateurs qui l'ont déjà.

Pas à l'aise avec Git ? Ouvrez simplement une *issue* en collant le contenu
du fichier : quelqu'un l'intégrera.

## Anatomie d'une recette

```json
{
  "id": "mon_jeu",
  "name": "Mon Jeu",
  "match": { "appid": ["1091500"] },
  "confidence": "exact",
  "derive": {
    "mode_ecran": { "from": "window_mode",
                    "map": { "fullscreen": "0", "borderless": "1" } }
  },
  "targets": [
    {
      "format": "ini",
      "paths": ["%LOCALAPPDATA%/MonJeu/Saved/Config/Windows/GameUserSettings.ini"],
      "entries": [
        { "section": "/Script/Engine.GameUserSettings",
          "key": "ResolutionSizeX", "value": "{resolution_w}",
          "label": "Largeur de l'image" }
      ]
    }
  ],
  "advice": ["Fermer le jeu avant d'appliquer les réglages."]
}
```

| Champ | Rôle |
|---|---|
| `match` | à quel jeu la recette s'applique : `appid`, `title`, `title_contains` ou `engine` |
| `confidence` | `exact`, `moteur` ou `generique` — sert à départager deux recettes |
| `derive` | traduit une valeur ORION en valeur attendue par le jeu |
| `targets` | les fichiers ou clés à écrire (`ini`, `registry`, `cfg`, `json`) |
| `advice` | conseils affichés à l'utilisateur sur la fiche du jeu |

**Variables de réglage** disponibles dans `value` : `resolution_w`,
`resolution_h`, `refresh`, `fps_cap`, `window_mode`, `vsync`, `quality`,
`q_textures`, `q_shadows`, `q_effects`, `q_postprocess`, `q_view_distance`,
`q_foliage`, `q_antialiasing`, `q_reflections`, `upscaler`, `frame_gen`,
`ray_tracing`, `reflex`, `fx_motion_blur`, `fx_bloom`, `fx_depth_of_field`,
`fx_film_grain`.

**Variables de chemin** disponibles dans `paths` : `install_dir`, `exe_dir`,
`localappdata`, `appdata`, `documents`, `saved_games`, `ue_project`,
`unity_company`, `unity_product`, plus les `%VARIABLES%` Windows et les
jokers `*`.

## Règles

- **Aucune donnée personnelle** : pas de chemin absolu contenant un nom
  d'utilisateur. Utilisez les variables ci-dessus.
- **Rien d'autre que des options graphiques.** Une recette ne touche ni aux
  sauvegardes, ni aux fichiers système, ni au réseau.
- **Testez avant de proposer.** ORION sauvegarde les fichiers avant chaque
  écriture, mais une mauvaise recette fait perdre du temps à tout le monde.

## Licence

Les recettes de ce dépôt sont publiées dans le domaine public (CC0) :
utilisez-les, modifiez-les, redistribuez-les librement.
<div align="center">

# ORION — Recettes communautaires

**La base de connaissances partagée du launcher ORION.**
Chaque recette apprend à l'application comment régler un jeu.

</div>

---

## C'est quoi ORION ?

Un launcher de jeux PC qui fait ce que les autres ne font pas : **il règle
les jeux à votre place**.

Il détecte tout ce qui est installé sur la machine — Steam, Epic, GOG,
Ubisoft, EA, Battle.net, Microsoft Store, et les jeux posés à la main dans un
dossier — récupère les jaquettes officielles, analyse le matériel et les
écrans, puis lance chaque jeu avec des réglages graphiques **calculés pour la
configuration réelle** et pour ce qu'on veut en faire : compétition, détente,
ou image maximale.

Gratuit, sans publicité, sans compte, sans télémétrie.

## Et ce dépôt, alors ?

ORION sait régler nativement les jeux Unreal Engine, Unity et Source. Pour
tous les autres — moteurs maison, jeux récents, cas particuliers — il a
besoin d'une **recette** : un petit fichier JSON qui lui dit où sont les
options du jeu et comment les écrire.

Une recette écrite par une personne sert à tout le monde. C'est le rôle de ce
dépôt : ORION lit `index.json` une fois par jour et télécharge les recettes
nouvelles ou mises à jour. Rien n'est envoyé depuis le poste de
l'utilisateur ; la synchronisation est en lecture seule.

## Proposer une recette

1. Dans ORION, ouvrez la fiche du jeu et cliquez sur **Partager cette
   recette** : deux fichiers sont créés dans votre dossier ORION.
2. Déposez `<id>.json` dans le dossier [`recipes/`](recipes/) de ce dépôt.
3. Ajoutez la ligne du fichier `<id>.index.json` dans
   [`index.json`](index.json).
4. Ouvrez une pull request.

Augmentez `version` d'une unité à chaque correction pour que la recette soit
redistribuée aux utilisateurs qui l'ont déjà.

Pas à l'aise avec Git ? Ouvrez simplement une *issue* en collant le contenu
du fichier : quelqu'un l'intégrera.

## Anatomie d'une recette

```json
{
  "id": "mon_jeu",
  "name": "Mon Jeu",
  "match": { "appid": ["1091500"] },
  "confidence": "exact",
  "derive": {
    "mode_ecran": { "from": "window_mode",
                    "map": { "fullscreen": "0", "borderless": "1" } }
  },
  "targets": [
    {
      "format": "ini",
      "paths": ["%LOCALAPPDATA%/MonJeu/Saved/Config/Windows/GameUserSettings.ini"],
      "entries": [
        { "section": "/Script/Engine.GameUserSettings",
          "key": "ResolutionSizeX", "value": "{resolution_w}",
          "label": "Largeur de l'image" }
      ]
    }
  ],
  "advice": ["Fermer le jeu avant d'appliquer les réglages."]
}
```

| Champ | Rôle |
|---|---|
| `match` | à quel jeu la recette s'applique : `appid`, `title`, `title_contains` ou `engine` |
| `confidence` | `exact`, `moteur` ou `generique` — sert à départager deux recettes |
| `derive` | traduit une valeur ORION en valeur attendue par le jeu |
| `targets` | les fichiers ou clés à écrire (`ini`, `registry`, `cfg`, `json`) |
| `advice` | conseils affichés à l'utilisateur sur la fiche du jeu |

**Variables de réglage** disponibles dans `value` : `resolution_w`,
`resolution_h`, `refresh`, `fps_cap`, `window_mode`, `vsync`, `quality`,
`q_textures`, `q_shadows`, `q_effects`, `q_postprocess`, `q_view_distance`,
`q_foliage`, `q_antialiasing`, `q_reflections`, `upscaler`, `frame_gen`,
`ray_tracing`, `reflex`, `fx_motion_blur`, `fx_bloom`, `fx_depth_of_field`,
`fx_film_grain`.

**Variables de chemin** disponibles dans `paths` : `install_dir`, `exe_dir`,
`localappdata`, `appdata`, `documents`, `saved_games`, `ue_project`,
`unity_company`, `unity_product`, plus les `%VARIABLES%' Windows et les
jokers `*`.

## Règles

- **Aucune donnée personnelle** : pas de chemin absolu contenant un nom
  d'utilisateur. Utilisez les variables ci-dessus.
- **Rien d'autre que des options graphiques.** Une recette ne touche ni aux
  sauvegardes, ni aux fichiers système, ni au réseau.
- **Testez avant de proposer.** ORION sauvegarde les fichiers avant chaque
  écriture, mais une mauvaise recette fait perdre du temps à tout le monde.

## Licence

Les recettes de ce dépôt sont publiées dans le domaine public (CC0) :
utilisez-les, modifiez-les, redistribuez-les librement.
