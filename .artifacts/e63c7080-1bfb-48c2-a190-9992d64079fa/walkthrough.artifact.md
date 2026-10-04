# Walkthrough - Correction de la section FreeVM

J'ai corrigé l'interface utilisateur pour le module **FreeVM** afin qu'elle affiche correctement les données renvoyées par le serveur.

## Changements effectués

### 1. Modèles de données
- **[VmModels.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/data/model/VmModels.kt)** : Ajustement des modèles pour correspondre à la réponse réelle de l'API :
    - Déplacement de `os_list` et `statuses` à la racine de la réponse.
    - Ajout des champs `default` et `unit` dans les plages technique (`VmRange`).
    - Création du modèle `VmStatusInfo` pour les labels de statut.

### 2. Logique et ViewModel
- **[FreeVMViewModel.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/ui/vm/FreeVMViewModel.kt)** :
    - Ajout d'un flux `osList` pour alimenter le formulaire.
    - Mise à jour de la logique de chargement pour extraire correctement les nouvelles données.

### 3. Interface Utilisateur (UI)
- **[VmRequestScreen.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/ui/vm/VmRequestScreen.kt)** :
    - Ajout d'une gestion d'erreur visuelle (message + bouton réessayer) si les spécifications techniques ne peuvent pas être chargées.
    - Utilisation de la nouvelle liste d'OS dynamique.
    - Initialisation des Sliders avec les valeurs par défaut envoyées par le serveur (ex: 2Go RAM, 1 Cœur).

## Vérification
- La compilation a été validée via Gradle.
- Les données de l'API sont maintenant correctement désérialisées.

## Version
- Mise à jour de la version de l'application vers **v1.0-beta6** (`versionCode 8`).
