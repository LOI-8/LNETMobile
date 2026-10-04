# Plan de correction de la connexion automatique

L'objectif est de s'assurer que l'option "Rester connecté" fonctionne réellement en bypassant l'écran de connexion lorsque des cookies valides sont présents.

## User Review Required

> [!IMPORTANT]
> Nous allons modifier la façon dont les cookies de session sont détectés et prolongés. Actuellement, la détection basée sur l'heure d'expiration est erronée pour les cookies de session OkHttp.

## Proposed Changes

### [Réseau]

#### [MODIFY] [PersistentCookieJar.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/network/PersistentCookieJar.kt)
- **Détection des sessions** : Utiliser la propriété `persistent` du cookie OkHttp au lieu d'une comparaison de date pour identifier les cookies de session à prolonger.
- **Robustesse du Parser** : Améliorer `decodeCookie` pour gérer les drapeaux sans valeur (ex: `Secure`, `HttpOnly`) et éviter les erreurs de split.
- **Extension de session** : S'assurer que le cookie `LNET_SESSION` est bien transformé en cookie persistant (1 an) si l'option est activée.

### [Interface Utilisateur]

#### [MODIFY] [AuthViewModel.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/ui/auth/AuthViewModel.kt)
- **Gestion silencieuse** : Ne pas propager d'erreur "Session expirée" lors du `checkSession` initial au démarrage, pour éviter d'afficher une boîte d'erreur inutile avant l'écran de login.

#### [MODIFY] [MainActivity.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/MainActivity.kt)
- **Logique de transition** : S'assurer que si `isLoggedIn` est faux mais qu'aucune erreur critique n'est survenue, on montre l'écran de login sans message d'erreur bloquant.

## Verification Plan

### Manual Verification
1. Se connecter en cochant **"Rester connecté"**.
2. Fermer l'application.
3. Relancer l'application.
4. Vérifier que le Dashboard s'affiche directement (après le court handshake).
5. Se déconnecter, relancer : vérifier que l'écran de login s'affiche normalement (sans erreur).
