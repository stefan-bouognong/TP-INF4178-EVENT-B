# Simulateur Event-B — Feux de signalisation (à partir des fichiers Rodin)

Application web autonome qui **anime votre modèle Rodin** (`Traffic_C0/C1`, `Traffic_M0/M1`)
directement à partir des fichiers sources `.buc`/`.bum`, avec un mini-animateur
Event-B (tokenizer + parseur + évaluateur ensembliste) qui applique **vos gardes et
actions exactes** et **vérifie les invariants** à chaque pas.

## Ouvrir

Double-cliquez sur **`index.html`** (ou glissez-le dans un navigateur : Chrome/Edge/Firefox).
Aucune installation, aucun serveur.

## Utiliser

- **Scène de trafic animée** : routes à deux voies, feux tricolores, véhicules qui
  circulent (axe vert) ou s'arrêtent avant le passage piéton (axe rouge), et piétons
  qui ne traversent que lorsque la voie est libre. Priorité piéton : les véhicules
  cèdent le passage si un piéton est en traversée.
- **Lancer la simulation** : mode « contrôleur » automatique — les phases s'alternent
  selon la durée de vert du modèle, les capteurs et règles floues font évoluer le trafic.
  *Réinitialiser* remet à l'état initial, *1 pas* franchit un seul événement, la
  glissière règle la vitesse.
- **Statistiques par voie** (panneau de droite) : état verbalisé de chaque voie (feu, trafic, file, durée de
  vert, chrono, piétons, priorité, attente) + **tableau en pourcentage** (% attente véhicules/piétons,
  % feu rouge, part de l'attente globale par voie).
- **Scénarios de trafic** : six profils prédéfinis (équilibré, axes chargés, piétons
  nombreux, heure de pointe, trafic faible). Choisir un scénario, *Appliquer*, puis
  *Lancer la simulation*.
- **Métriques en direct** : temps d'attente global des véhicules et des piétons
  (secondes cumulées + moyenne par entité).
- **Grille de performance** : comparer les scénarios sur les deux métriques d'attente.
  *Enregistrer ce scénario* après une course, ou *Comparer tous les scénarios* pour
  remplir automatiquement la grille (45 s par scénario).
- **Onglets `Traffic_M0` / `Traffic_M1`** : M1 = raffinement avec chronomètres et `TICK`.
- **Événements activables / État brut / Invariants / Trace ProB / Modèle** : panneau
  en bas de page pour inspecter le modèle Event-B.

> **Axes de phase.** Le modèle Rodin n'actionne qu'une voie représentative par axe
> (Nord pour N–S, Est pour E–O) ; dans la scène, Sud partage la phase de Nord et Ouest
> celle d'Est, pour un carrefour réaliste. Les variables brutes restent visibles dans
> l'onglet « État brut ».

## Importer vos propres fichiers

Bouton **« 📂 Importer le dossier TrafficClean »** : sélectionnez le dossier du projet
Rodin ; l'appli reparse les vrais `.buc`/`.bum` (et une éventuelle `.prob2trace`).
Par défaut, une copie de vos fichiers est embarquée (`model_data.js`) pour un démarrage
immédiat.

## Conformité vérifiée

Le moteur a été validé en rejouant la trace ProB existante : **19/19 comparaisons
d'état identiques à ProB, 0 divergence, 31/31 invariants évalués et satisfaits**. Ce
que vous voyez correspond donc exactement au modèle vérifié dans Rodin.

## Fichiers

- `index.html` — application (moteur + interface), tout-en-un.
- `model_data.js` — copie embarquée des fichiers Rodin (générée depuis `TrafficClean/`).
# TP-INF4178-EVENT-B
