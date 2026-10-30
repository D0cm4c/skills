# Skills

Dépôt de skills (protocoles réutilisables) pour les sessions IA travaillant sur l'écosystème **Atelier du web**.

## Index des skills

| Skill | Objectif | Déclencheur |
|---|---|---|
| [coordination-intersessions](coordination-intersessions/SKILL.md) | Coordonner plusieurs sessions IA travaillant en parallèle sur des dépôts liés, via des issues GitHub | Projet multi-dépôts travaillés par plusieurs sessions IA |

## Mode d'emploi

Pour appliquer un skill, ouvre une session IA dans le dépôt concerné et indique-lui :

> Suis le skill coordination-intersessions du dépôt D0cm4c/skills

La session lira le protocole complet dans `coordination-intersessions/SKILL.md` et copiera la section `templates/AGENTS-PROTOCOL.md` dans le `AGENTS.md` de chaque dépôt de l'écosystème.

## Écosystème Atelier du web

- `D0cm4c/Gestion-Membres-Inscriptions-de-l-Atelier-du-web` — app de gestion des membres (repo **app**)
- `D0cm4c/atelierduweb-mec-api` — plugin WordPress (repo **plugin**)
- `D0cm4c/skills` — ce dépôt (protocoles transverses)

## Conventions

- Commits en français, préfixés par type : `feat:`, `docs:`, `fix:`, `refactor:`
- Une demande inter-dépôts = une issue GitHub, jamais de modification directe dans un dépôt partenaire
