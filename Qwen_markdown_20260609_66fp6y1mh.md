# 📊 Trading Journal Pro (PWA)

Une application web progressive (PWA) professionnelle, conçue pour les traders qui souhaitent suivre rigoureusement leurs performances, gérer leur risque et analyser leurs setups. 

L'application fonctionne **entièrement hors-ligne**, s'installe comme une application native sur votre téléphone (Android/iOS), et utilise une architecture de navigation imbriquée ("poupées russes") pour une organisation optimale.

---

## ✨ Fonctionnalités Principales

- 📱 **100% Mobile & Hors-ligne** : S'installe sur l'écran d'accueil et fonctionne sans connexion internet grâce au Service Worker.
- 🪆 **Navigation "Poupées Russes"** : Tableau de Bord → Mois → Semaine (continue de 1 à 53) → 8 Trades max par semaine.
- 🧮 **Calculateur Intelligent** : Calcule automatiquement la taille du lot et le P&L réalisé en fonction de votre balance, de votre risque (%) et de votre ratio R:R (TP/SL).
- 📸 **Journal Visuel** : Possibilité d'ajouter des captures d'écran "Avant" (Setup) et "Après" (Résultat) directement depuis la galerie du téléphone.
- 📈 **Statistiques en Temps Réel** : Win Rate, nombre de gains/pertes, total des pips TP/SL par semaine.
- 💾 **Sauvegarde Portable** : Export et Import de toutes vos données au format JSON (votre base de données personnelle).
- 🎨 **Design Professionnel** : Interface "Dark Mode" moderne, épurée et optimisée pour le trading.

---

## 🛠️ Stack Technique

- **Frontend** : HTML5, CSS3 (Variables, Flexbox, Grid), Vanilla JavaScript (Aucun framework lourd).
- **Stockage** : `localStorage` du navigateur (pour une utilisation immédiate et hors-ligne).
- **PWA** : `manifest.json` et `sw.js` (Service Worker) pour la mise en cache et l'installation mobile.

---

## 🚀 Installation et Utilisation

### 1. Hébergement (GitHub Pages)
Ce projet est conçu pour être hébergé gratuitement sur GitHub Pages :
1. Les fichiers `index.html`, `manifest.json` et `sw.js` doivent être à la racine du dépôt.
2. Activez GitHub Pages dans les `Settings` > `Pages` > Branche `main`.

### 2. Installation sur Mobile (Pour en faire une "App")
Une fois le lien de votre GitHub Pages ouvert :

**Sur Android (Chrome) :**
1. Ouvrez le lien dans Chrome.
2. Appuyez sur les **3 points** (⋮) en haut à droite.
3. Sélectionnez **"Ajouter à l'écran d'accueil"** ou **"Installer l'application"**.

**Sur iPhone (Safari) :**
1. Ouvrez le lien dans Safari.
2. Appuyez sur le bouton **Partager** (carré avec une flèche vers le haut).
3. Faites défiler et sélectionnez **"Sur l'écran d'accueil"**.

---

## 📖 Guide d'Utilisation Rapide

1. **Configuration Initiale** : Lors de la première ouverture, entrez votre balance de départ et votre risque par trade en pourcentage (ex: 1% ou 2%).
2. **Navigation** : Choisissez un mois, puis une semaine (le calendrier suit un format continu de 53 semaines par an).
3. **Ajouter un Trade** : Cliquez sur un emplacement vide (maximum 8 par semaine).
4. **Saisie** : Remplissez les détails. Le **Lot** et le **P&L** se calculent automatiquement dès que vous entrez le SL et le TP. Vous pouvez ajuster manuellement le P&L si nécessaire (slippage, sortie partielle).
5. **Sauvegarde** : Cliquez sur "Enregistrer". La balance globale se met à jour instantanément.

---

## ⚠️ IMPORTANT : Gestion des Données

> **Note cruciale** : Cette application utilise le `localStorage` de votre navigateur. Cela signifie que vos données sont stockées **localement sur votre appareil**. 
> - Si vous videz le cache de votre navigateur, vous perdrez vos données.
> - **Bonne pratique** : Cliquez régulièrement sur le bouton **"💾 Exporter JSON"** et conservez ce fichier sur votre téléphone ou envoyez-le vous par email. 
> - Pour restaurer vos données sur un nouvel appareil, utilisez le bouton **"Importer JSON"**.

---

## 📂 Structure des Fichiers

```text
├── index.html       # Structure et logique principale de l'application
├── manifest.json    # Configuration de l'application PWA (nom, icône, thème)
├── sw.js            # Service Worker pour la mise en cache et le mode hors-ligne
└── README.md        # Ce fichier de documentation