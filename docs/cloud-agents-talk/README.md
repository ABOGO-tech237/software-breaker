# Cloud Agents — talk Cursor Cameroun

**Quand :** samedi 19 septembre 2026 · **~15–20 min** · **français**  
**Fichiers :** slides HTML locales + notes + sources. Rien à merger dans `main` si tu n’en as pas besoin.

## Ouvrir les slides

Depuis ce dossier :

```bash
cd docs/cloud-agents-talk
python3 -m http.server 8765
```

Puis ouvrir [http://localhost:8765/](http://localhost:8765/).

Sans serveur : double-clic sur `index.html` (`file://`). Le deck est autonome (pas de CDN).

| Fichier | Rôle |
| --- | --- |
| [index.html](index.html) | Diapos + notes orateur intégrées |
| [NOTES.md](NOTES.md) | Script linéaire (imprime ou second écran) |
| [SOURCES.md](SOURCES.md) | Docs officielles + ce que la VM a (ou n’a pas) vu |

## Présenter

1. Plein écran : `F` ou `F11`.
2. Avancer : `→` `Espace` `Entrée` · Reculer : `←` `Backspace`.
3. Notes : `N` (ou clic sur « Notes »).
4. Aide : `?`.
5. Viser **~45–60 s** par slide produit, **~75 s** par cas.

Le public Cursor Cameroun connaît déjà l’agent **local**. Insiste sur la différence : **même agent, autre machine**, branche isolée, PR à relire.

## 3 démos live (préparer avant)

### 1. Lancer un Cloud Agent (obligatoire)

Depuis Cursor Desktop : menu **Cloud** sous le champ agent.  
Ou [cursor.com/agents](https://cursor.com/agents). Compte **payant** + Git connecté (docs).

Prompt prêt à coller (repo `Delmat237/Cursor-Cameroun`, **ne pas merger dans `main` sans relecture**) :

```text
Sur une branche cloud, ajoute un événement « Talk Cloud Agents · Yaoundé »
daté du samedi 19 septembre 2026 dans src/data/events.json (status upcoming).
Recalcule les status : tout événement dont endDateISO < 2026-09-19
ne doit plus être upcoming. N’invente pas de Luma. Ouvre une PR draft.
Ne merge pas.
```

Montre : VM qui démarre → commits sur **autre branche** → PR draft.

### 2. Cette run comme preuve

Ouvre [cette run](https://cursor.com/agents/bc-af5de014-b7c3-4e96-a308-ef22f425faf7) ou la PR de ce dossier.

À dire : le Cloud Agent n’a **pas** vu `/home/atangana/Projects/...`. Il a cloné les remotes publics, déclaré les 404, et livré le talk sur **sa** branche. C’est le modèle : isolation, pas le laptop du speaker.

### 3. Computer Use / bureau distant

Docs officielles : l’agent pilote souris/clavier/navigateur ; tu peux **prendre le bureau distant** puis le lui rendre. Le libellé **« Try Live » n’est pas dans les docs** — si tu le vois dans l’UI, c’est ce contrôle-là.

Cible simple : [cursor-cameroun-nine.vercel.app](https://cursor-cameroun-nine.vercel.app) — bascule FR/EN, Events, thème.  
Ou, si l’environnement EatNext est prêt : recherche resto + fiche (sans inventer un résultat).

Plan B si le bureau distant est lent : montrer les **artefacts** (captures / vidéo) d’une run déjà finie.

## Ce qu’il ne faut pas dire

- Pas de métriques inventées (« +40 % », « l’agent a fixé EatNext »).
- Pas de stack inventée pour **mobileAI**, **openSpace**, **crew**.
- Pas « Try Live » comme nom produit officiel.
- Cloud Agents = plan payant ; auto-fix CI GitHub Actions = **Teams**, PRs **créées par l’agent**.

## Durée

| Bloc | Temps |
| --- | --- |
| Titre + enjeu | 2 min |
| Produit (slides 3–9) | 7 min |
| Cas réels (10–16) | 7 min |
| Démos + close | 3–4 min |
| **Total** | **~16–20 min** |

Si tu débordes : saute MobiYaounde + Openspace (une phrase : « remotes inaccessibles, voir SOURCES ») et garde Cursor-Cameroun + software-breaker + EatNext.
