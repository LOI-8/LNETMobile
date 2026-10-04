# Ajout de l'interface utilisateur pour le module FreeVM

Ce plan détaille l'implémentation de la section **FreeVM** dans l'interface utilisateur de l'application, permettant aux utilisateurs de commander et de suivre leurs machines virtuelles.

## User Review Required

> [!IMPORTANT]
> L'interface permettra de :
> 1. Voir la liste des demandes de VM avec leur statut en temps réel.
> 2. Créer une nouvelle demande via un formulaire dynamique (basé sur les spécifications de l'API).
> 3. Consulter les détails d'une VM, incluant une barre de progression visuelle (étapes 1 à 5) et les identifiants d'accès SSH/RDP une fois la VM active.

## Proposed Changes

### [Component] Logic (ViewModel)

#### [NEW] [FreeVMViewModel.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/ui/vm/FreeVMViewModel.kt)
- Gestion de l'état des demandes de VM.
- Récupération des spécifications techniques pour le formulaire.
- Logique de création de demande.

#### [MODIFY] [ViewModelFactory.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/ui/ViewModelFactory.kt)
- Ajout du support pour `FreeVMViewModel`.

---

### [Component] UI (Screens)

#### [NEW] [VmListScreen.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/ui/vm/VmListScreen.kt)
- Liste des VMs avec badge de statut coloré.
- Bouton "+" pour créer une nouvelle demande.

#### [NEW] [VmRequestScreen.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/ui/vm/VmRequestScreen.kt)
- Formulaire avec Sliders pour RAM/CPU/Disque (respectant les min/max de l'API).
- Liste déroulante pour le choix de l'OS.

#### [NEW] [VmDetailScreen.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/ui/vm/VmDetailScreen.kt)
- Affichage de la frise de progression (Step 1 à 5).
- Affichage sécurisé des identifiants `access_id` et `access_password`.

---

### [Component] Navigation

#### [MODIFY] [MainScreen.kt](file:///C:/Users/Compt/AndroidStudioProjects/LNET/app/src/main/java/com/loi/lnet/ui/main/MainScreen.kt)
- Ajout de `Screen.VM` dans la barre de navigation basse.
- Ajout de la carte "Cloud VM" dans le Dashboard.
- Configuration des routes NavHost pour les 3 nouveaux écrans VM.

## Verification Plan

### Automated Tests
- Lancement de `app:assembleDebug` pour valider la compilation.

### Manual Verification
- Naviguer vers la nouvelle section VM.
- Vérifier que le formulaire de création affiche bien les bonnes plages de valeurs (ex: RAM 1-8 Go).
- Simuler/Vérifier l'affichage d'une VM "Active" avec ses accès.
