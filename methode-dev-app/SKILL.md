---
name: methode-dev-app
description: Méthode complète pour concevoir et développer une application (desktop, web, mobile) avec un porteur de projet, notamment non technique — du cadrage par la discussion au code, en passant par un benchmark, des specs écrites, un phasage et une revue critique. À appliquer dès le démarrage d'un nouveau projet d'application, avant toute ligne de code.
user-invocable: true
license: MIT
---

# Skill : methode-dev-app

Concevoir et développer une application étape par étape : comprendre le problème réel, décider l'architecture la plus simple pour l'utilisateur, écrire les specs, se les faire relire/critiquer, puis coder par phases démontrables.

## Déclencheur

Nouveau projet de création d'application, avec un porteur de projet (client, fondateur, utilisateur cible). Dès le premier échange, avant tout code.

## Problème résolu

Coder sans cadrage produit des applications inutiles, trop complexes ou jamais terminées. Cette méthode impose de **discuter, documenter et valider avant d'écrire du code**, avec des documents vivants dans `docs/`, et une livraison propre (branches, PR).

## Les phases

### Phase 1 — Comprendre (discussion uniquement, aucun code)

- Vision + problème + cible, en 3 phrases maximum
- Personas croisés, **ancrés sur des recherches web avec des chiffres récents** (ex. : % de temps passé en administratif par les indépendants, impayés, etc.)
- Benchmark des solutions existantes : tableau comparatif par catégorie + checklist des fonctionnalités « standard du marché » → en déduire la **différenciation réelle** et les oublis
- Écrire 3 à 5 **principes directeurs** (ex. : « desktop installable », « débutant d'abord », « rien ne bouge sans validation », « toujours chiffré »)

### Phase 2 — Choisir l'architecture la plus simple pour l'utilisateur

- Tableau des connecteurs (mail, stockage, chat…) avec protocole/API pour chacun
- **Privilégier les protocoles ouverts** (IMAP/SMTP, WebDAV, dossier local) pour éviter tout « compte développeur » côté utilisateur en MVP ; les API officielles (OAuth) en option plus tard, documentées
- Sécurité dès le départ : secrets uniquement dans `.env` (gitignoré), tokens chiffrés via `safeStorage`, base chiffrée (SQLCipher + mot de passe maître **systématique**, même en local), cache des pièces jointes chiffré

### Phase 3 — Écrire les specs dans `docs/` (documents vivants, poussés en PR draft)

- `README.md` : vision, piliers, principes directeurs
- `docs/architecture.md` : stack, connecteurs, données, sécurité
- `docs/onboarding.md` : parcours de premier lancement (une question par écran, « Plus tard » partout)
- `docs/ecran-accueil.md` : le point pivot de l'app, justifié par les personas
- `docs/concurrents.md` : le benchmark
- un doc par domaine fonctionnel (classement de fichiers, notes, tâches, fiche client, synchro chiffrée…)
- `docs/phasage.md` : M0 → Mn, chaque étape démontrable
- `docs/spec-fonctionnelle-M0-M1.md` : user stories, **écrans en wireframes textuels**, parcours détaillés, cas d'erreur, critères d'acceptation, hors-scope déclaré
- `docs/schema-bdd.md` : schéma SQL complet

### Phase 4 — Revue critique avant tout code

Relire toutes les specs, se les critiquer soi-même : incohérences corrigées, oublis notés, **questions ouvertes tranchées avec le porteur** (ex. : chiffrement systématique ? plusieurs projets par client ? étiquettes libres ?). Document : `docs/revue-specs.md`.

### Phase 5 — Livraison GitHub

- Branche `vibe/<slug>-9cb977`, commits en français préfixés (`feat:`, `docs:`, `fix:`), PR **draft**
- **Ne coder que ce qui est écrit dans la spec**

### Phase 6 — Code par phases (M0…Mn)

Chaque phase se termine par quelque chose de démontrable ; si la cible est débutante, chaque phase est testée avec un profil débutant.

## Règles UX si la cible est débutante

- Une seule question par écran, gros boutons explicites, langage clair (jamais de jargon)
- « Plus tard » toujours proposé ; l'app doit fonctionner sans aucun compte externe
- Aucune action sur les données de l'utilisateur sans clic de validation (mode prudent par défaut)
- Erreurs expliquées en langage clair + nouvelle tentative guidée, jamais un code d'erreur brut
- Rappels / encouragements doux, jamais bloquants, désactivables dans les réglages

## Cas limites

| Cas | Action |
|---|---|
| Le porteur veut coder tout de suite | Insister sur le cadrage : un MVP mal cadré coûte 10× plus cher en refontes |
| La fonctionnalité demandée contredit un principe directeur | Le signaler explicitement, arbitrage humain |
| La recherche web ne tranche pas une question | Poser la question au porteur avec 2–4 options concrètes |
| Besoin d'une API officielle (ex. Gmail API) | L'activer en option documentée (compte développeur), pas en prérequis du MVP |

## Exemple réel

Projet « Fusion Indépendant » (app desktop pour indépendant) : 15 documents de cadrage dans `docs/`, PR draft, décisions tranchées (base + cache toujours chiffrés, multi-projets par client, étiquettes libres, MVP zéro compte développeur via IMAP/SMTP + WebDAV/local).

## Limites connues

- Ralentit le démarrage (quelques jours de cadrage) mais évite les refontes
- Nécessite un porteur disponible pour répondre aux questions ouvertes et valider les specs
