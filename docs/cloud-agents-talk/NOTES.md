# Notes orateur — Cloud Agents · 19 sept. 2026

Script ~16–18 min. Les slides portent déjà un résumé ; ici c’est le fil à voix haute.

## 1. Titre (~30 s)

« On va parler des Cloud Agents Cursor, avec nos vrais repos — pas un deck générique. Tout fait produit vient des docs cursor.com. Si je n’ai pas pu ouvrir un repo, je le dis. »

## 2. Enjeu (~45 s)

L’agent local est déjà utile. Le plafond : un seul laptop, des conflits de fichiers, et tu dois rester en ligne. Le cloud enlève ça : une VM par tâche, plusieurs agents en parallèle, le laptop peut se couper.

## 3. Agenda (~20 s)

Trois blocs : le produit tel que documenté ; cinq projets à nous ; trois démos dont un lancement réel.

## 4. Définition (~50 s)

Même fondamentaux d’agent, **autre machine**. VM Ubuntu isolée : clone, deps, secrets, réseau. Elle peut builder, tester, cliquer l’UI. Ancien nom : Background Agents.

## 5. Cloud vs local (~70 s)

Local = ton checkout (ou un **worktree** git isolé). Cloud = clone **depuis Git**, état propre distant. « Move to Cloud » **ne prend pas** tes fichiers non commités — stash/commit d’abord. Worktrees : parallèle **sur le laptop**. Cloud : parallèle **sans le laptop**.

## 6. Boucle (~60 s)

Start → VM isolée → clone → travail sur **branche séparée** → push → **PR draft** → humain relit. Rien ne merge tout seul. Commits signés (clé HSM Ed25519, badge Verified). MicroVM Firecracker ; un agent ne voit pas l’autre.

## 7. Lancer (~50 s)

Desktop : Cloud sous le champ. Web : cursor.com/agents. Aussi iOS, Slack `@cursor`, GitHub/Bitbucket `@cursor` sur issue/PR, Linear, API. CLI : préfixer `&`. Automations : cron ou événements. Il faut un **plan payant** et le SCM connecté par un admin.

## 8. Computer Use (~50 s)

Souris, clavier, navigateur dans la VM. Dev server → clics → artefacts (captures, vidéos, logs) sur la PR. **Bureau distant** : tu prends la main, tu rends. Je n’ai pas trouvé « Try Live » dans les docs.

## 9. Bons usages (~40 s)

Feature / bug / tests hors ligne. Plusieurs agents. Vérif UI. Multi-repos (PRs coordonnées ; long-running pas encore). Relancer depuis Slack/GitHub. Auto-fix CI sur **ses** PRs (GHA, Teams).

## 10. Limites (~70 s)

Environnement mal préparé = agent à moitié aveugle. Pas de dirty local. Hooks `~/.cursor` absents (skills perso : Sync Skills). CI auto : Teams + GHA + PR agent. Pièces jointes web 4 / 15 Mo. Injection de prompt + egress : allowlist. Humain sur la PR. Sibling paths : **cette run ne voyait pas** `/home/atangana/Projects`.

## 11. Méthode cas (~30 s)

Inspecté = clone ou checkout. Sinon on le dit. crew : pas de remote inventé.

## 12. Cursor-Cameroun (~75 s)

Site Next.js 16, FR/EN, events JSON, carte, admin. Tâche concrète : événement du 19 sept. + status périmés (Café Douala et Meetup juillet encore `upcoming` dans le JSON du 18 sept.). Computer Use : FR/EN, Events, thème. README vs AGENT.md pas d’accord sur la carte 10 régions — l’agent peut mesurer, pas inventer le score.

## 13. software-breaker (~60 s)

Skill + subagent Full Chaos, déjà dans **ce** repo. Tâche : lancer le chaos sur un module, rapport bilingue reproductible, **pas de fix auto**. Cette présentation est elle-même une run cloud sur ce repo.

## 14. MobiYaounde (~40 s)

`ABOGO-tech237/mobileAI` : 404 ici. Pas de stack inventée. Pour demain : connecter le repo privé à l’environnement Cloud Agents, puis « explore et propose une PR draft ».

## 15. EatNext (~75 s)

Public vu : `ABOGO-tech237/EatNext` (le remote `studio-crafiti/EatNext` est 404). Monorepo Express/Prisma + Vite, Postgres/Redis, Ayilaa. Notion : découverte + avis, Crafti, Yaoundé. Tâche : environnement avec secrets DB, un flux recherche→fiche→avis, PR vers `develop`. On n’a **pas** exécuté l’app ici.

## 16. Openspace (~25 s)

`openSpace` introuvable. Même discipline : connecter, ne pas raconter un résultat.

## 17. crew (~15 s)

Pas de dossier local. Omis.

## 18. Preuve de la run (~45 s)

URL de l’agent, branche isolée, docs sous `docs/cloud-agents-talk/`. C’est le talk.

## 19. Démos (~2 min + live)

Les trois du README. Si le réseau lâche : artefacts + cette PR.

## 20. Close (~30 s)

Cloud = isolation + vérification + PR. Local = itération sous tes yeux. On choisit selon la tâche, pas par mode.

## 21. Sources + questions

Renvoyer à SOURCES.md. Question fréquente : « c’est moins sûr ? » — les docs disent **profil de risque différent**, pas pire : sandbox + egress vs laptop ouvert.
