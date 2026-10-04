# Suspension de compte et Mise à jour API v1

J'ai intégré le support pour la suspension de compte et mis à jour l'application pour utiliser les nouveaux standards de l'API v1.

## Changements effectués

### 1. Gestion des erreurs et suspension
- **Parsing intelligent** : L'application ne se contente plus de dire "Identifiants incorrects". Elle parse maintenant le corps d'erreur JSON (même sur les erreurs 403) pour extraire l' `error_code` et la `reason`.
- **Détection Anti-Bot** : Si le serveur renvoie du HTML au lieu de JSON, l'application affiche désormais un message clair suggérant un problème d'Anti-Bot au lieu d'afficher une erreur de parsing technique.
- **Écran de suspension** : Si un compte est désactivé (`account_disabled`), un écran bloquant s'affiche avec la raison fournie par l'administrateur.

### 2. Mise à jour de l'API
- **Modèles de données** : Ajout de `errorCode` et `reason` dans `MeResponse` et `SimpleResponse`.
- **Nouveaux endpoints** : Ajout des structures pour les futurs écrans de contacts, préférences de profil et notifications.

### 3. Fiabilisation du réseau
- Centralisation de la gestion des réponses dans `AuthRepository` pour garantir une détection cohérente de l'état de la session et de la suspension.

## Ce qui a été testé
- **Build OK** : Le projet compile parfaitement.
- **Logique de détection** : Le Repository est maintenant capable de différencier un JSON d'erreur d'une page HTML.

> [!IMPORTANT]
> Pour tester l'écran de suspension, le serveur doit renvoyer un code HTTP `403` avec un corps JSON contenant `"error_code": "account_disabled"`. L'application passera alors automatiquement sur l'écran d'alerte.

render_diffs(file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/data/AuthRepository.kt)
render_diffs(file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/ui/auth/SuspendedScreen.kt)
