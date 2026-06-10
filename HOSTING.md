# Hébergement de la politique de confidentialité

⚠️ Aucun dépôt Git / remote GitHub n'est configuré dans ce projet (`git remote -v`
échoue avec « not a git repository »). Impossible donc de configurer GitHub Pages
automatiquement. Le dossier `website/` (avec `index.html` qui redirige vers
`privacy.html`) est prêt à être déployé tel quel sur n'importe quel hébergeur
statique. Voici les 3 options les plus simples, de la plus rapide à mettre en
place à la plus durable.

## Option 1 — Netlify Drop (le plus rapide, 0 compte requis pour tester)

1. Aller sur https://app.netlify.com/drop
2. Glisser-déposer le dossier `website/` (contenant `index.html` et `privacy.html`)
3. Netlify génère immédiatement une URL du type `https://random-name.netlify.app`
4. Pour une URL stable, créer un compte gratuit (sinon le site peut expirer après
   un certain temps) puis renommer le site dans **Site settings → General → Site details**
5. Copier l'URL `https://<nom-du-site>.netlify.app/privacy.html` et la renseigner dans :
   - Play Console → fiche de l'app → "Politique de confidentialité"
   - Google Cloud → OAuth consent screen → "Privacy Policy URL"

## Option 2 — Vercel (compte gratuit, déploiement par CLI ou drag & drop)

1. Créer un compte sur https://vercel.com (gratuit)
2. Installer la CLI : `npm i -g vercel`
3. Depuis le dossier `website/` : `vercel --prod`
4. Suivre les instructions (premier déploiement = config par défaut)
5. Vercel fournit une URL `https://<projet>.vercel.app`
6. URL finale : `https://<projet>.vercel.app/privacy.html`

## Option 3 — GitHub Pages (le plus durable, nécessite un dépôt GitHub)

1. Créer un dépôt sur https://github.com/new (ex. `inkletter-app`)
2. Initialiser Git dans le projet et pousser le contenu :
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin https://github.com/<user>/inkletter-app.git
   git push -u origin main
   ```
3. Dans **Settings → Pages** du dépôt :
   - Source : `Deploy from a branch`
   - Branch : `main` (ou `gh-pages`), dossier `/website` (ou `/docs` si renommé)
   - Si l'option "dossier custom" n'est pas disponible pour `/website`, créer une
     branche `gh-pages` ne contenant que le contenu de `website/` à la racine,
     ou copier `website/*` dans un dossier `/docs` à la racine du dépôt.
4. URL générée : `https://<user>.github.io/inkletter-app/privacy.html`
   (ou `https://<user>.github.io/inkletter-app/` si `index.html` redirige déjà
   vers `privacy.html`, ce qui est le cas ici)
5. Une fois l'URL connue, mettre à jour :
   - `app.config.ts` : ajouter l'URL publique (ex. dans un commentaire ou une
     constante `extra.privacyPolicyUrl`) pour référence
   - `app/privacy.tsx` : ajouter un lien externe vers cette URL en complément
     du texte in-app
   - Play Console et Google Cloud OAuth consent screen (cf. `docs/PRODUCTION.md`)

## Recommandation

Pour aller vite aujourd'hui : **Option 1 (Netlify Drop)** suffit pour obtenir une
URL valide à coller dans Play Console et Google Cloud. Si un dépôt GitHub est créé
plus tard pour le code source du projet, basculer vers **Option 3 (GitHub Pages)**
pour une URL plus pérenne et versionnée avec le code.
