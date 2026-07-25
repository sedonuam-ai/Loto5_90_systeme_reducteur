# SAME GLOBAL SERVICES — Système réducteur Loto 5/90

Application Android **100% hors-ligne**, thème sombre, pour le Loto 5/90 :
- Génération automatique de 180 grilles de 5 numéros (1 à 90), triés
- Vérification instantanée d'un tirage officiel contre les 180 grilles (saisie avec passage automatique au champ suivant)
- Statistiques (répartitions 2/3/4/5 bons numéros, fréquences, paires, triplets) + réinitialisation
- Historique des tirages + réinitialisation
- Export PDF / Excel (CSV) et impression
- Toutes les données sont stockées uniquement sur le téléphone (base Room/SQLite locale), **aucune permission Internet dans le manifeste**
- Logo et icône de lancement dédiés (monogramme SGS)

## Installer l'APK depuis GitHub (sans Android Studio)

1. Créez un dépôt GitHub (public ou privé) et poussez ce dossier dedans :
   ```bash
   cd LottoApp
   git init
   git add .
   git commit -m "Loto 5/90 - version initiale"
   git branch -M main
   git remote add origin https://github.com/VOTRE-COMPTE/loto590.git
   git push -u origin main
   ```
2. Dès que le push est terminé, GitHub lance automatiquement la compilation
   (fichier `.github/workflows/build.yml`, onglet **Actions** du dépôt).
   Cela prend 2 à 4 minutes.
3. Une fois le workflow terminé (coche verte ✅) :
   - Onglet **Releases** (à droite de la page du dépôt) → téléchargez `app-debug.apk`
   - ou onglet **Actions** → cliquez sur le run → section *Artifacts* → `Loto590-debug-apk`
4. Transférez le fichier `.apk` sur votre téléphone Android (câble, e-mail à vous-même, Drive…).
5. Sur le téléphone, ouvrez le fichier `.apk` pour l'installer. Android demandera
   d'autoriser "l'installation d'applications inconnues" pour l'application utilisée
   (Fichiers, Gmail, Chrome...) — c'est normal pour un APK qui ne vient pas du Play Store.
6. L'application s'installe et fonctionne entièrement hors connexion.

## Compiler soi-même avec Android Studio (alternative)

1. `File > Open` → sélectionner le dossier `LottoApp`
2. Laisser Android Studio synchroniser Gradle (nécessite Internet la première fois,
   pour télécharger les dépendances — l'application elle-même n'en a jamais besoin)
3. `Run ▶` sur un émulateur ou un téléphone branché en USB (mode développeur + débogage USB actifs)

## Structure du projet

```
app/src/main/java/com/lottoapp180/
├── data/        Room (base locale) : entités Grille/Tirage, DAO, Repository
├── logic/       Génération des grilles, vérification, statistiques
├── export/      Export PDF (natif Android) et Excel/CSV
└── ui/          Écrans Compose, navigation, ViewModels
```

## Personnaliser la plage de numéros

Le jeu est actuellement paramétré pour le Loto 5/90 (5 numéros parmi 1 à 90).
Pour changer de variante, modifiez uniquement les constantes en tête de
`app/src/main/java/com/lottoapp180/logic/GrilleGenerator.kt` :

```kotlin
const val MIN_NUMERO = 1
const val MAX_NUMERO = 90
const val NUMEROS_PAR_GRILLE = 5
```
