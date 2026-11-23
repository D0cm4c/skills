---
name: pre-production
description: Encadrer toute phase de conception AVANT tout codage — cadrage du besoin, exploration des options, pour/contre documentés, document de conception, décisions figées et validation humaine. Généralisation de la leçon « charte avant maquette » : « conception avant code ». À invoquer dès qu'un nouveau chantier, une nouvelle fonctionnalité majeure, un changement d'architecture ou une maquette est envisagé, avant d'écrire la moindre ligne de code.
user-invocable: true
license: MIT
---

# Skill : pre-production

Toute phase de conception doit être **cadrée par écrit et validée par l'humain AVANT d'écrire du code**. Ce skill encadre cette phase de pré-production, quel que soit le chantier : nouvelle fonctionnalité, refonte, changement d'architecture, design, synchronisation de données…

**Règle fondatrice** : *conception avant code* — une leçon généralisée de la méthode design validée sur l'écosystème Atelier du web (« charte avant maquette », leçon n° 20 du dépôt app : une règle écrite = un jugement objectif). Le doc de conception vient APRÈS la discussion si le porteur veut comprendre et peser, AVANT le code toujours.

## Déclencheur

- Un chantier est évoqué («_sync multi-postes», «nouvelle page», «on refait le design de X») sans décision figée.
- L'utilisateur demande à comprendre, comparer des options, ou « peser le pour/contre ».
- Avant toute maquette, POC ou code sur un chantier non encore documenté.

## Problème résolu

Coder avant de cadrer produit des chantiers refaits, des options non comparées en silence, et des décisions implicites que personne ne peut relire ou auditer. Ici : **tout chantier naît dans un document comparé et signé** (validé dans la conversation), pas dans du code.

## Les étapes (dans l'ordre, aucune ne s'autorise à sauter)

### 1. Cadrer le besoin (en une page maximum)

- **Le problème réel** en 3 phrases : qui, quoi, pourquoi maintenant.
- **Périmètre** : ce qui est dedans, ce qui est explicitement dehors.
- **Contraintes figées** existantes (architecture, sécurité, design, budget, hébergement) — les relire depuis la mémoire du projet (CONTEXT.md, AGENTS.md, chartes).

### 2. Explorer les options (minimum 2, idéalement 3)

Pour chaque option : un nom parlant, une explication **compréhensible par un non-technicien**, et ce qu'elle implique concrètement (infra, dépendances, coût de maintenance, migration).

- Chercher d'abord ce qui existe déjà (registre de skills, bibliothèques, docs du projet, le web) avant d'inventer.
- Identifier les **pièges connus** de chaque option (ex. données binaires + synchro de fichiers = corruption potentielle).

### 3. Documenter le pour/contre (tableau comparatif)

Un tableau : lignes = critères pertinents (simplicité pour l'utilisateur, robustesse, sécurité, coût, migration future…) ; colonnes = options. Ensuite une **recommandation argumentée** — la session propose, l'humain décide.

### 4. Poser les questions ouvertes

- Toute question non tranchée est **posée explicitement avec 2–4 options concrètes**, jamais résolue en silence par la session.
- Aucune boucle : si la décision nécessite un tiers (hébergeur, DPO, associé), le noter comme **bloquant externe** et continuer sur le reste.

### 5. Rédiger le document de conception

`docs/conception/<slug-du-chantier>.md` (ou à l'emplacement équivalent du projet), contenant :

1. Besoin et périmètre
2. Options explorées + tableau pour/contre
3. **Décisions figées** (nivelées une par une, avec leur raison) — marquées ⚠️ tant que l'humain n'a pas dit « go »
4. Schéma/flux de données si applicable
5. Questions ouvertes / bloqueurs externes
6. Plan de livraison (phases démontrables, une fonctionnalité par PR)

### 6. Validation humaine, puis code

- **Le document est présenté à l'utilisateur et explicitement validé AVANT tout code.** « Normalement tu sais quoi faire » n'est pas une validation de conception.
- Une fois validé : les décisions deviennent figées, recopiées dans la mémoire du projet (CONTEXT.md), et le code suit le plan, phase par phase.
- Si le porteur veut coder tout de suite : insister une fois avec le coût du recadrage (un chantier mal cadré coûte 10× plus cher en refontes), puis respecter sa décision s'il maintient.

## Règles de sécurité de la phase

- **Aucune décision d'interface, de schéma ou de sécurité n'est prise en silence** : format, noms de champs, routes, clés — tout est écrit.
- Jamais de secret dans un doc de conception (le chiffrement est décrit, les clés ne le sont jamais).
- La gouvernance (sécurité, production, données personnelles) reste **humaine**.
- Compatibilité avec l'existant : chaque option est évaluée contre les décisions déjà figées (le nouveau ne casse pas le validé — ex. ne pas toucher au design desktop validé).

## Anti-patterns (refusés par ce skill)

| Anti-pattern | Correction |
|---|---|
| Coder "un petit POC" pour voir | Cadrer d'abord ; le POC est une phase du plan, documenté |
| Une seule option présentée | Minimum 2 options comparées |
| Pour/contre dans la tête de la session | Tableau écrit dans le doc, relisible par tous |
| Décision figée sans « go » explicite | Marquée ⚠️ en attente, jamais codée |
| Doc de conception rédigé AVANT la discussion si le porteur veut discuter | Discuter d'abord, documenter ensuite (mais toujours avant le code) |

## Exemple réel

Chantier « sync chiffrée multi-postes » du dépôt maquette Atelier du web (nov. 2026) : le porteur veut comprendre la technique avant tout. La session ne code pas ; elle pose les pistes (A : dump chiffré AES-GCM + WebDAV Nextcloud, avec le piège identifié SQLite-binaire + sync de fichiers = corruption ; B : app locale Tauri ; C : backend SQLite partagé), la question CORS reste ouverte, et la décision est reportée au porteur. Le doc de conception viendra après la discussion — pas avant, pas jamais à la place du code.
