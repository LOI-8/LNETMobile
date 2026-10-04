# Walkthrough - Version 1.0-preview

Les modifications pour la version `1.0-preview` ont été appliquées avec succès.

## Changements effectués

### Configuration
- **Version** : Le `versionName` a été mis à jour à `1.0-preview` dans [build.gradle.kts](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/build.gradle.kts).

### Interface Utilisateur (UI)
- **Barre de navigation inférieure** : La `NavigationBar` a été retirée de l'écran principal [MainScreen.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/ui/main/MainScreen.kt).
- **Service de Chat** : Toutes les références au service de Chat ont été supprimées :
    - Retrait du raccourci sur le tableau de bord (Dashboard).
    - Suppression des écrans de chat du graphe de navigation.
    - Nettoyage des imports et du ViewModel associé.
- **Navigation améliorée** : Un bouton de retour a été ajouté dans la barre supérieure (`TopAppBar`). Ce bouton apparaît automatiquement dès que l'utilisateur quitte le Dashboard, permettant de revenir facilement à l'accueil.

## Vérification
- La compilation du projet via Gradle (`:app:assembleDebug`) a réussi, confirmant l'absence d'erreurs de syntaxe ou de références manquantes.
- Le nettoyage de `ViewModelFactory.kt` a été effectué pour éviter d'instancier un `ChatViewModel` désormais inutile.

> [!NOTE]
> L'application repose désormais sur le **Dashboard** comme centre de navigation principal.
