[README.md](https://github.com/user-attachments/files/22480679/README.md)
# FaceID-Jeu — package prêt à héberger (GitHub Pages)

Ce package contient une page web statique qui **simule** un déverrouillage par reconnaissance faciale (Face-ID) en comparant la photo de référence fournie avec un scan effectué par la caméra du navigateur.

## Contenu du ZIP
- `index.html` — page de scan (utilise `face-api` via CDN).
- `unlocked.html` — page affichée après déverrouillage réussi.
- `images/camille.png` — photo de référence (à placer devant la caméra pour déverrouiller).
- `README.md` — ce fichier.

## Déploiement (pas à pas) — sur GitHub Pages
1. Crée un compte GitHub si tu n'en as pas.  
2. Crée un nouveau repository (par ex. `faceid-game`).  
3. Dans ton dépôt, clique sur **Add file → Upload files** et glisse le contenu du ZIP (ou téléverse l'archive et clique pour extraire).  
4. Une fois les fichiers présents, va dans **Settings → Pages**.  
   - Choisis la branche `main` (ou `master`) et le dossier `/ (root)` si demandé.  
   - Clique sur **Save**. Quelques minutes plus tard ton site sera disponible à :  
     `https://<ton-identifiant>.github.io/<nom-de-repo>/`  
   - Accède à `https://<ton-identifiant>.github.io/<nom-de-repo>/index.html`

> Note : GitHub Pages sert via HTTPS — nécessaire pour activer la caméra dans la plupart des navigateurs.

## Tester localement (optionnel)
Pour tester sur ta machine sans GitHub Pages, il te faut servir les fichiers via HTTP (la caméra et face-api exigent un contexte sécurisé ou HTTP sur localhost) :
```bash
cd faceid_game
python3 -m http.server 8000
# puis ouvrir http://localhost:8000/index.html
```

## Ajustements et conseils
- **Seuil (`THRESHOLD`)** : par défaut `0.6`. Pour photos imprimées il faut souvent être plus permissif (→ `0.6–0.7`). Pour de la vraie biométrie tu baisserais le seuil (plus strict). Teste et ajuste.  
- **Photo de référence** : si le script n'arrive pas à détecter un visage, recadre l'image sur le visage, augmente la résolution, et évite ombres/filtres.  
- **Permissions caméra** : autorise l'accès à la caméra (popup du navigateur). Si la page est servie via `file://`, la caméra sera bloquée — utilise GitHub Pages ou `http.server`.  
- **Google Sites** : héberge sur GitHub Pages et intègre la page dans Google Sites via un <iframe> (ou lien direct).

## Sécurité & confidentialité
Tout le traitement est effectué localement dans le navigateur : aucune image n'est envoyée à un serveur par le code fourni. Toutefois, les modèles `face-api` sont chargés depuis un CDN.

## Problèmes fréquents et solutions rapides
- *La caméra ne démarre pas* → vérifier HTTPS / localhost et permissions.  
- *Aucun visage détecté* → recadrer la photo / augmenter luminosité / rapprocher la photo de la caméra.  
- *Détection trop stricte* → augmenter la valeur THRESHOLD dans `index.html`.
