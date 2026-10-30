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

## Activer coordination-intersessions par défaut sur tous tes projets

Le skill suit le standard ouvert **Agent Skills** (dossier + `SKILL.md` avec frontmatter YAML, `user-invocable: true`), donc directement compatible avec Vibe Code CLI et le Chat/Work Mistral.

### Vibe Code CLI — actif dans tous les projets

Installe-le au **niveau utilisateur** (`~/.vibe/skills/`) : il est découvert automatiquement dans chaque session, quel que soit le projet, sans rien ajouter par projet.

```bash
git clone https://github.com/D0cm4c/skills.git /tmp/skills-repo
mkdir -p ~/.vibe/skills
cp -r /tmp/skills-repo/coordination-intersessions ~/.vibe/skills/
rm -rf /tmp/skills-repo
```

Vérification : dans une session Vibe, tape `/` — le skill `coordination-intersessions` doit apparaître dans la liste des commandes slash. Tu peux aussi simplement le mentionner (« utilise le skill coordination-intersessions ») ou laisser Vibe l'activer automatiquement quand la tâche correspond à sa description.

Mise à jour : `git pull` du dépôt puis re-copier le dossier.

Alternative : `./.vibe/skills/` ou `./.agents/skills/` dans chaque projet (suivi par Git, revu en PR) — à réserver aux projets de l'écosystème.

### Chat / Vibe Work (chat.mistral.ai)

1. Onglet **Work** → panneau latéral → **Contexte** → **Skills** → **Nouveau skill**
2. **Titre** : `Coordination inter-sessions` ; **Description** : copier la description du frontmatter ci-dessus
3. **SKILL.md** : coller le contenu de `coordination-intersessions/SKILL.md` (sans le frontmatter)
4. Joindre `templates/AGENTS-PROTOCOL.md` comme fichier support
5. **Créer le skill** → bouton **Partager** → **Espace de travail** (actif pour toute l'équipe)

Un admin peut ensuite le **forcer** pour tout l'espace via les réglages d'administration (il devient alors toujours actif, non désactivable).

## Écosystème Atelier du web

- `D0cm4c/Gestion-Membres-Inscriptions-de-l-Atelier-du-web` — app de gestion des membres (repo **app**)
- `D0cm4c/atelierduweb-mec-api` — plugin WordPress (repo **plugin**)
- `D0cm4c/skills` — ce dépôt (protocoles transverses)

## Conventions

- Commits en français, préfixés par type : `feat:`, `docs:`, `fix:`, `refactor:`
- Une demande inter-dépôts = une issue GitHub, jamais de modification directe dans un dépôt partenaire
