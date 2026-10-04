# Plan de passage en version 1.0-preview

Ce plan détaille les modifications nécessaires pour préparer la version `1.0-preview` de l'application LNET, conformément à la demande de retrait de la barre de navigation inférieure et du service de Chat.

## Modifications proposées

### [Configuration du projet]

#### [MODIFY] [build.gradle.kts](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/build.gradle.kts)
- Mise à jour de `versionName` à `"1.0-preview"`.

### [UI Principale]

#### [MODIFY] [MainScreen.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/ui/main/MainScreen.kt)
- **Suppression du Chat** :
    - Retrait de `Screen.Chat` de la liste des écrans.
    - Suppression de l'initialisation de `chatViewModel`.
    - Retrait des routes `Screen.Chat.route` et `chat_detail` du `NavHost`.
    - Suppression du `ServiceItem` "Chat" dans `DashboardContent`.
- **Suppression de la barre du bas** :
    - Retrait du paramètre `bottomBar` dans le `Scaffold` de `MainScreen`.
- **Navigation** :
    - Ajout d'une icône de navigation (flèche retour) dans la `TopAppBar` de `MainScreen` lorsque l'utilisateur n'est pas sur le tableau de bord (`Screen.Dashboard`). Cette icône permettra de revenir au `Dashboard`.

### [Nettoyage]

#### [MODIFY] [ViewModelFactory.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/ui/ViewModelFactory.kt)
- Retrait de la création de `ChatViewModel` (optionnel).

## Plan de vérification

### Tests manuels
- Déploiement de l'application sur un émulateur/appareil.
- Vérification que la version affichée (si applicable) ou interne est `1.0-preview`.
- Vérification de l'absence de la `NavigationBar` en bas de l'écran.
- Vérification de l'absence du service "Chat" sur le tableau de bord.
- Vérification que la navigation vers les autres services (Mail, Sites, etc.) fonctionne depuis le Dashboard.
- Vérification que le bouton "Retour" apparaît dans la barre du haut sur ces services et permet de revenir au Dashboard.
