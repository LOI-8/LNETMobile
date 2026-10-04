# Mémorisation de session (Rester connecté)

L'application permet désormais de rester connecté durablement grâce à une nouvelle option dédiée.

## Fonctionnalités ajoutées

### 1. Option "Rester connecté"
- **Nouveauté** : Une case à cocher est désormais disponible sur les écrans de **Connexion** et d'**Inscription**.
- **Effet** : Si cochée, l'application sauvegarde vos identifiants de session (cookies) avec une validité étendue (1 an).

### 2. Persistance de session intelligente
- **Gestionnaire de cookies** : Le `PersistentCookieJar` a été amélioré. Il détecte maintenant le cookie `LNET_SESSION` et le transforme en cookie permanent si l'option est activée.
- **Auto-reconnexion** : Au lancement, l'application utilise automatiquement les cookies sauvegardés pour vous emmener directement sur le Dashboard sans demander de mot de passe.

### 3. Sécurité et Contrôle
- **Expiration** : Les cookies restent valables tant qu'ils ne sont pas invalidés par le serveur ou que vous ne vous déconnectez pas manuellement.
- **Nettoyage** : Cliquer sur "Déconnexion" efface totalement les cookies et réinitialise l'option de mémorisation.

## Comment utiliser
1. Sur l'écran de connexion, cochez **"Rester connecté"**.
2. Identifiez-vous.
3. Fermez l'application et relancez-la : vous arrivez directement sur vos messages !

> [!TIP]
> N'utilisez cette option que sur votre téléphone personnel pour garantir la sécurité de votre compte.
