# Protocole inter-sessions (à copier dans chaque AGENTS.md)

> Copier la section ci-dessous dans le `AGENTS.md` de chaque dépôt de l'écosystème,
> en adaptant le nom du dépôt partenaire. Protocole complet : skill
> `coordination-intersessions` du dépôt `D0cm4c/skills`.

## Protocole de coordination inter-sessions

Ce dépôt fait partie d'un écosystème multi-dépôts travaillé par plusieurs sessions IA.
Le protocole de coordination est défini dans le skill `coordination-intersessions`
du dépôt `D0cm4c/skills` et se résume ainsi :

- **Au démarrage** : lister les issues ouvertes sur ce dépôt **et** sur le dépôt
  partenaire (`gh issue list --repo <owner>/<repo> --state open`). Traiter en
  priorité les issues portant le label `pour-<ce-dépôt>`.
- **Traitement d'une issue** : commenter d'abord son plan, livrer, puis fermer
  l'issue en citant le commit/PR.
- **Demande vers le partenaire** : ouvrir une issue sur le dépôt cible avec le
  label `pour-<cible>` et un titre préfixé `[<ce-dépôt>]`, contenant contexte,
  spec précise (routes/formats/exemples) et critère d'acceptation.
- **Interfaces** : toute décision d'interface (nom de champ, route, format) est
  documentée dans les **deux** dépôts.
- **Interdits** : jamais de secret dans une issue ; jamais de modification directe
  d'un dépôt partenaire ; pas de boucle d'issues (renvoi mutuel → arbitrage humain).
- **Gouvernance** : sécurité, production et produit restent des décisions humaines.

Partenaire(s) de ce dépôt : `<owner>/<dépôt-partenaire>` (label `pour-<partenaire>`).
