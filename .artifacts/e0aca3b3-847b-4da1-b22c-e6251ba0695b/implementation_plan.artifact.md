# Plan d'implémentation : Suspension de compte et Mise à jour API v1

Ce plan détaille les modifications nécessaires pour intégrer le système de suspension de compte et mettre à jour l'application avec les nouveaux endpoints de l'API v1 décrits dans la documentation.

## User Review Required

> [!IMPORTANT]
> - L'application affichera désormais un écran bloquant si le compte est détecté comme désactivé (`account_disabled`).
> - La gestion des erreurs a été centralisée pour extraire les codes d'erreur et les raisons fournies par le serveur.

## Proposed Changes

### [Component] Data Models

#### [MODIFY] [AuthModels.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/data/model/AuthModels.kt)
- Ajouter `errorCode` (error_code) et `reason` aux réponses d'authentification.
- Mettre à jour `SimpleResponse` pour inclure ces champs.

#### [NEW] [ProfileModels.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/data/model/ProfileModels.kt)
- Modèles pour les préférences de profil et le changement de mot de passe.

#### [NEW] [ContactModels.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/data/model/ContactModels.kt)
- Modèles pour la gestion des contacts et l'annuaire.

#### [NEW] [NotificationModels.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/data/model/NotificationModels.kt)
- Modèles pour les notifications.

### [Component] Network & API

#### [MODIFY] [LnetApiService.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/network/LnetApiService.kt)
- Ajouter les nouveaux endpoints :
    - `/mail/search-users`
    - `/profile/password`
    - `/profile/prefs`
    - `/contacts` (GET, POST, DELETE)
    - `/notifications` (GET, unread-count)

#### [MODIFY] [NetworkModule.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/network/NetworkModule.kt)
- Exposer l'instance `Json` pour permettre le parsing des corps d'erreur dans les repositories.

### [Component] Repositories

#### [MODIFY] [AuthRepository.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/data/AuthRepository.kt)
- Implémenter une méthode `parseError` pour extraire `errorCode` et `reason` des réponses d'erreur (4xx/5xx).
- Ajouter un `StateFlow` pour l'état de suspension du compte.

#### [NEW] [ContactsRepository.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/data/ContactsRepository.kt)
#### [NEW] [NotificationRepository.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/data/NotificationRepository.kt)

### [Component] UI

#### [MODIFY] [AuthViewModel.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/ui/auth/AuthViewModel.kt)
- Gérer l'état de suspension et exposer la raison.

#### [NEW] [SuspendedScreen.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/ui/auth/SuspendedScreen.kt)
- Écran affiché lorsque le compte est désactivé.

#### [MODIFY] [MainActivity.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/MainActivity.kt)
- Intégrer la vérification de l'état suspendu dans le flux principal de l'application.

## Verification Plan

### Automated Tests
- Vérifier que le parsing du JSON avec `error_code` et `reason` fonctionne.

### Manual Verification
- Simuler une réponse 403 avec `error_code: "account_disabled"` pour vérifier l'affichage de l'écran de suspension.
- Vérifier que les nouveaux endpoints sont bien appelés (via logs).
