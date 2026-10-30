# Skill : coordination-intersessions

Coordonner plusieurs sessions IA travaillant en parallèle sur des dépôts liés d'un même écosystème, en remplaçant « l'humain-bus-de-données » par des issues GitHub.

## Déclencheur

Appliquer ce skill dès qu'un projet est multi-dépôts (par ex. une app + un plugin + un dépôt transverse) et que plusieurs sessions IA peuvent y travailler en parallèle — chaque session étant rattachée à un dépôt.

## Problème résolu

L'humain-bus-de-données : sans protocole, l'humain copie-colle manuellement les demandes, specs et résultats entre sessions/dépôts. C'est lent, sujet aux oublis et aux erreurs.

Leçon réelle (exemple concret) : l'app envoyait le champ `adw_name` alors que le plugin attendait `adw_nom` — la modale restait vide. Chaque session connaissait son propre format, mais personne ne documentait l'interface dans les deux dépôts. Ce protocole impose une documentation croisée de toute décision d'interface.

## Mise en place (une fois par écosystème)

1. Copier le contenu de `templates/AGENTS-PROTOCOL.md` dans le `AGENTS.md` de **chaque** dépôt de l'écosystème, en adaptant le nom du dépôt partenaire.
2. Créer sur chaque dépôt un label `pour-<dépôt-partenaire>` pour chaque partenaire :
   ```bash
   gh label create "pour-app" --repo <owner>/<repo> --description "Demande à traiter par la session du dépôt app" --color "0e8a16"
   gh label create "pour-plugin" --repo <owner>/<repo> --description "Demande à traiter par la session du dépôt plugin" --color "5319e7"
   ```
3. Tester la boucle complète : ouvrir une issue « bonjour 👋 » sur le dépôt cible avec son label, vérifier que la session partenaire la traite et la ferme.

## Règles au démarrage de chaque session

1. Lister les issues ouvertes **sur son dépôt** : `gh issue list --repo <owner>/<mon-dépôt> --state open`
2. Lister aussi les issues ouvertes **sur les dépôts partenaires** : `gh issue list --repo <owner>/<partenaire> --state open`
3. Traiter en priorité les issues portant **son** label `pour-<mon-dépôt>` (elles sont adressées à cette session).
4. Pour chaque issue à traiter : **commenter d'abord son plan** (compréhension, fichiers visés, plan de livraison), puis livrer, puis **fermer l'issue** en citant le commit/PR de livraison.
5. Pour ses propres demandes inter-dépôts : ouvrir une issue sur le dépôt cible avec le label `pour-<cible>` et un titre préfixé `[<mon-dépôt>]`.

## Rédaction d'une demande inter-dépôts

Une demande = une issue, contenant :

- **Contexte** : dépôt émetteur, session émettrice, dépôt cible
- **Spec précise** : routes, formats, noms de champs, exemples de payloads (ex. `adw_nom`, pas `adw_name`)
- **Critère d'acceptation** : comment la session cible vérifie que la demande est satisfaite

Règles de rédaction :

- Toute décision d'interface (nom de champ, route, format) est documentée **dans les deux dépôts** (issue + AGENTS.md ou doc de chaque côté).
- **Jamais de secret dans une issue** (token, mot de passe, clé, `.env`).
- Pas de boucle : si deux issues se renvoient mutuellement la responsabilité (A renvoie à B, B renvoie à A), **demander l'arbitrage humain** plutôt que de créer une nouvelle issue.
- La gouvernance (sécurité, production, produit) reste **humaine** : une session IA ne déploie pas, ne publie pas, ne supprime pas de données de production.

## Cas limites

| Cas | Action |
|---|---|
| Issue ambiguë ou incomplète | Commenter l'issue pour demander la précision à la session émettrice ; ne pas improviser la spec |
| Demande hors périmètre de mon dépôt | Commenter l'issue en l'expliquant et la faire renvoyer vers le bon dépôt (ou arbitrage humain) |
| Deux issues incompatibles entre elles | Mettre en évidence le conflit dans un commentaire sur chaque issue ; arbitrage humain |
| Pas de session partenaire active | Traiter les issues de son côté si possible ; sinon laisser l'issue ouverte avec un commentaire d'état |

## Exemple réel : écosystème Atelier du web

- Dépôts : `app` (Gestion-Membres-Inscriptions-de-l-Atelier-du-web) et `plugin` (atelierduweb-mec-api)
- Labels : `pour-app` / `pour-plugin` (créés sur le repo app)
- Exemple app→plugin : demande d'endpoint `/wp-json/adw-mec/v1/labels` (commit `b143c62`), issue ouverte sur le repo app avec label `pour-plugin`, spec précisant la route et le format attendus.

## Limites connues

- Repose sur la lecture des `AGENTS.md` par chaque session ; si un `AGENTS.md` manque, le protocole ne s'applique pas dans ce dépôt.
- GitHub only : le transport des demandes est exclusivement des issues GitHub.
- Asynchrone : une session ne peut pas forcer une autre à traiter une issue ; les échanges sont retardés par les temps de session respectifs.
