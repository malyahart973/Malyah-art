# Malyah Art — Gestion atelier (PWA)

Application de gestion d'atelier : produits, matières premières, recettes,
production, caisse, achats, clients, fournisseurs, traçabilité, étiquettes
et rapports.

## Déployer sur GitHub Pages (sans ligne de commande)

1. Sur [github.com](https://github.com), créez un nouveau dépôt **public**
   (ex. `malyah-art`).
2. Sur la page du dépôt, cliquez **Add file → Upload files**.
3. Glissez-déposez les 7 fichiers de ce dossier :
   `index.html`, `manifest.json`, `service-worker.js`, `icon-192.png`,
   `icon-512.png`, `icon-512-maskable.png`, `favicon.png`.
4. Cliquez **Commit changes**.
5. Allez dans **Settings → Pages**. Sous « Build and deployment »,
   choisissez **Deploy from a branch**, branche `main`, dossier `/ (root)`,
   puis **Save**.
6. Au bout d'une à deux minutes, votre application est en ligne à l'adresse
   `https://<votre-nom-utilisateur>.github.io/malyah-art/`.

## Installer l'application (PWA)

Une fois le lien ci-dessus ouvert :
- **Android (Chrome)** : menu ⋮ → « Installer l'application » (ou bannière automatique).
- **iPhone/iPad (Safari)** : bouton Partager → « Sur l'écran d'accueil ».
- **Ordinateur (Chrome/Edge)** : icône d'installation dans la barre d'adresse.

L'application fonctionne alors hors-ligne, avec sa propre icône, sans barre
de navigateur.

## ⚠️ À savoir sur les données

Par défaut, cette version GitHub Pages **n'a pas de compte ni de sauvegarde
cloud** : chaque appareil/navigateur garde ses propres données en local. La
section suivante explique comment activer une vraie synchronisation
automatique entre vos appareils via Google Drive — sinon, faites des
sauvegardes régulières avec le bouton *Exporter (JSON)* de l'onglet
**Sauvegarde**, et *Importer* pour recharger vos données sur un autre
appareil.

## Activer la synchronisation automatique (Google Drive)

L'application sait se synchroniser via un fichier privé dans votre Google
Drive (invisible dans vos dossiers habituels, accessible uniquement par
cette app). Il faut d'abord créer un identifiant OAuth gratuit chez Google —
10 minutes, une seule fois :

1. Allez sur [console.cloud.google.com](https://console.cloud.google.com/)
   et créez un nouveau projet (ex. « Malyah Art »).
2. Menu **APIs & Services → Library**, cherchez **Google Drive API**,
   cliquez **Enable**.
3. Menu **APIs & Services → OAuth consent screen** :
   - Type d'utilisateur : **External**.
   - Renseignez un nom d'app (« Malyah Art ») et votre e-mail.
   - Sous **Scopes**, ajoutez `.../auth/drive.appdata`.
   - Sous **Test users**, ajoutez votre propre adresse e-mail Google.
   - Une fois créé, sur la page du consentement, cliquez **Publish app**
     (statut « In production ») pour éviter que l'accès n'expire au bout
     de 7 jours — pas besoin de validation Google pour ce type d'usage.
4. Menu **APIs & Services → Credentials → Create credentials → OAuth
   client ID** :
   - Type d'application : **Web application**.
   - Sous **Authorized JavaScript origins**, ajoutez
     `https://<votre-nom-utilisateur>.github.io`.
   - Cliquez **Create** : Google affiche un **Client ID** qui ressemble à
     `123456789-abc...apps.googleusercontent.com`. Copiez-le.
5. Dans `index.html` (sur GitHub, cliquez le fichier puis l'icône crayon
   pour l'éditer directement dans le navigateur), cherchez la ligne :
   ```js
   const GOOGLE_CLIENT_ID = "VOTRE_CLIENT_ID.apps.googleusercontent.com";
   ```
   et remplacez la valeur par votre Client ID copié à l'étape 4. **Commit
   changes.**
6. Rechargez l'application, ouvrez l'onglet **Sauvegarde**, cliquez
   **Connecter Google Drive**, acceptez l'accès. Répétez cette connexion
   une fois sur chaque appareil (téléphone, ordinateur) — ensuite, toutes
   les données se synchronisent automatiquement entre eux.

Le Client ID n'est pas un secret (c'est le cas pour toutes les apps web
Google) : il peut rester visible dans le code sans risque.

## Mettre à jour l'application

Pour publier une nouvelle version (après une modification du code) :
1. Remplacez les fichiers modifiés dans le dépôt GitHub (Upload files à
   nouveau, ou éditez-les directement dans l'interface GitHub).
2. Dans `service-worker.js`, changez la valeur de `CACHE_VERSION`
   (ex. `malyah-art-v2`) pour forcer la mise à jour chez les utilisateurs
   qui ont déjà installé l'app.

## Fichiers

| Fichier | Rôle |
|---|---|
| `index.html` | L'application complète (React, autonome) |
| `manifest.json` | Déclare l'app comme installable (nom, icônes, couleurs) |
| `service-worker.js` | Permet le fonctionnement hors-ligne |
| `icon-*.png`, `favicon.png` | Icônes de l'application |

## Charte graphique — v3

La version harmonisée reprend les codes visuels du logo et de la capture de référence :
- bleu pétrole / marine profond pour la navigation et les zones structurantes ;
- turquoise / cyan de la résine pour les actions, indicateurs et accents ;
- fonds blancs et bleu très pâle pour conserver la lisibilité ;
- cartes plus aérées, angles plus doux et ombres discrètes ;
- zone de marque Malyah Art renforcée dans la navigation ;
- barre supérieure et états actifs avec accents turquoise ;
- cache PWA incrémenté en `malyah-art-v3` pour forcer la prise en compte du nouveau thème.
