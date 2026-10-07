# Deux poids, deux mesures

Interface mobile avec réponses en grille 2 × 2, retour visuel au toucher, questions courtes et détails des résultats dépliables.

Application statique bilingue français/anglais : dix questions, cinq paires comparables, révélation finale et partage du tirage exact. Aucun compte, serveur de résultats, suivi, stockage des réponses ou API payante. Les réponses restent en mémoire dans l’onglet. Les polices sont locales.

## Développement

Node.js 20.19+ ou 22.12+ (validé avec Node 24).

```sh
npm ci --cache /workspace/.npm-cache
npm run dev
```

## Vérification et publication

```sh
npm test
npm run build
npx playwright test
```

Les tests navigateur utilisent Chromium installé dans `/usr/bin/chromium` dans cet environnement. Adapter `playwright.config.js` sur une autre machine. Le dossier `dist/` est publiable sur un hébergeur statique. Le site est publié sur https://tomwillg.github.io/Ai/.

## Scénarios

`src/scenarios.js` contient 200 dilemmes bilingues : 25 thèmes avec huit situations distinctes par thème. Chaque entrée isole deux identités et conserve exactement les mêmes faits et les mêmes choix. Chaque scène met en balance plusieurs priorités (règle, exception, coût, vérification, délai) avec quatre actions concrètes. La pertinence psychologique de cette rédaction n’a pas fait l’objet d’une validation scientifique. Les sujets graves sont non graphiques et évitables. Les résultats ne constituent pas un diagnostic ou un instrument scientifique validé.

Le tirage sélectionne cinq thèmes distincts. L’ordre de la seconde moitié varie. Au moins deux autres questions séparent les deux versions d’une situation. La place des options change entre les variantes, tout en gardant leurs identifiants sémantiques pour comparer les réponses. Un remplacement modifie les deux versions avant la première réponse; une paire déjà commencée ne peut plus être remplacée. Le mode sans violence exclut agressions, violences sexuelles et abus sur mineurs.

Les liens de défi encodent les dix questions et leur ordre, jamais les réponses. Conserver les identifiants et l’ordre de la banque pour ne pas invalider les liens existants.

## GitHub Pages

Le workflow `.github/workflows/pages.yml` vérifie et compile le site, puis publie `dist/` à chaque mise à jour de `main`. Dans les paramètres du dépôt GitHub, section **Pages**, sélectionner **GitHub Actions** comme source. Les chemins d’assets sont relatifs pour fonctionner sous `/Ai/` ou sur un domaine personnalisé. L’URL publique est confirmée uniquement après un déploiement réussi.
