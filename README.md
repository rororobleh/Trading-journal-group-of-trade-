[README(2).md](https://github.com/user-attachments/files/28869280/README.2.md)
# 📊 Trading Journal Pro (PWA)

---

## 🇫🇷 Français

Une application web progressive (PWA) professionnelle, conçue pour les traders qui souhaitent suivre rigoureusement leurs performances, gérer leur risque et analyser leurs setups.

L'application fonctionne **entièrement hors-ligne**, s'installe comme une application native sur votre téléphone (Android/iOS), et utilise une architecture de navigation imbriquée ("poupées russes") pour une organisation optimale.

### ✨ Fonctionnalités Principales

- 📱 **100% Mobile & Hors-ligne** : S'installe sur l'écran d'accueil et fonctionne sans connexion internet grâce au Service Worker.
- 🪆 **Navigation "Poupées Russes"** : Tableau de Bord → Mois → Semaine (continue de 1 à 53) → 8 Trades max par semaine.
- 🧮 **Calculateur Intelligent** : Calcule automatiquement la taille du lot et le P&L réalisé en fonction de votre balance, de votre risque (%) et de votre ratio R:R (TP/SL).
- 📸 **Journal Visuel** : Possibilité d'ajouter des captures d'écran "Avant" (Setup) et "Après" (Résultat) directement depuis la galerie du téléphone.
- 📈 **Statistiques en Temps Réel** : Win Rate, nombre de gains/pertes, total des pips TP/SL par semaine.
- 💾 **Sauvegarde Portable** : Export et Import de toutes vos données au format JSON (votre base de données personnelle).
- 🎨 **Design Professionnel** : Interface "Dark Mode" moderne, épurée et optimisée pour le trading.

### 🛠️ Stack Technique

- **Frontend** : HTML5, CSS3 (Variables, Flexbox, Grid), Vanilla JavaScript (Aucun framework lourd).
- **Stockage** : `localStorage` du navigateur (pour une utilisation immédiate et hors-ligne).
- **PWA** : `manifest.json` et `sw.js` (Service Worker) pour la mise en cache et l'installation mobile.

### 🚀 Installation et Utilisation

#### 1. Hébergement (GitHub Pages)
Ce projet est conçu pour être hébergé gratuitement sur GitHub Pages :
1. Les fichiers `index.html`, `manifest.json` et `sw.js` doivent être à la racine du dépôt.
2. Activez GitHub Pages dans les `Settings` > `Pages` > Branche `main`.

#### 2. Installation sur Mobile (Pour en faire une "App")
Une fois le lien de votre GitHub Pages ouvert :

**Sur Android (Chrome) :**
1. Ouvrez le lien dans Chrome.
2. Appuyez sur les **3 points** (⋮) en haut à droite.
3. Sélectionnez **"Ajouter à l'écran d'accueil"** ou **"Installer l'application"**.

**Sur iPhone (Safari) :**
1. Ouvrez le lien dans Safari.
2. Appuyez sur le bouton **Partager** (carré avec une flèche vers le haut).
3. Faites défiler et sélectionnez **"Sur l'écran d'accueil"**.

### 📖 Guide d'Utilisation Rapide

1. **Configuration Initiale** : Lors de la première ouverture, entrez votre balance de départ et votre risque par trade en pourcentage (ex: 1% ou 2%).
2. **Navigation** : Choisissez un mois, puis une semaine (le calendrier suit un format continu de 53 semaines par an).
3. **Ajouter un Trade** : Cliquez sur un emplacement vide (maximum 8 par semaine).
4. **Saisie** : Remplissez les détails. Le **Lot** et le **P&L** se calculent automatiquement dès que vous entrez le SL et le TP. Vous pouvez ajuster manuellement le P&L si nécessaire (slippage, sortie partielle).
5. **Sauvegarde** : Cliquez sur "Enregistrer". La balance globale se met à jour instantanément.

### ⚠️ IMPORTANT : Gestion des Données

> **Note cruciale** : Cette application utilise le `localStorage` de votre navigateur. Cela signifie que vos données sont stockées **localement sur votre appareil**.
> - Si vous videz le cache de votre navigateur, vous perdrez vos données.
> - **Bonne pratique** : Cliquez régulièrement sur le bouton **"💾 Exporter JSON"** et conservez ce fichier sur votre téléphone ou envoyez-le vous par email.
> - Pour restaurer vos données sur un nouvel appareil, utilisez le bouton **"Importer JSON"**.

### 📂 Structure des Fichiers

```text
├── index.html       # Structure et logique principale de l'application
├── manifest.json    # Configuration de l'application PWA (nom, icône, thème)
├── sw.js            # Service Worker pour la mise en cache et le mode hors-ligne
└── README.md        # Ce fichier de documentation
```

---

## 🇬🇧 English

A professional progressive web app (PWA) designed for traders who want to rigorously track their performance, manage their risk, and analyze their setups.

The app works **entirely offline**, installs like a native app on your phone (Android/iOS), and uses a nested "Russian doll" navigation architecture for optimal organization.

### ✨ Main Features

- 📱 **100% Mobile & Offline**: Installs on your home screen and works without an internet connection thanks to the Service Worker.
- 🪆 **"Russian Doll" Navigation**: Dashboard → Month → Week (continuous from 1 to 53) → Up to 8 trades per week.
- 🧮 **Smart Calculator**: Automatically calculates lot size and realized P&L based on your balance, risk (%), and R:R ratio (TP/SL).
- 📸 **Visual Journal**: Add "Before" (setup) and "After" (result) screenshots directly from your phone's gallery.
- 📈 **Real-Time Statistics**: Win rate, number of wins/losses, total TP/SL pips per week.
- 💾 **Portable Backup**: Export and import all your data as JSON (your personal database).
- 🎨 **Professional Design**: Modern, clean "Dark Mode" interface optimized for trading.

### 🛠️ Tech Stack

- **Frontend**: HTML5, CSS3 (Variables, Flexbox, Grid), Vanilla JavaScript (no heavy framework).
- **Storage**: Browser `localStorage` (for immediate, offline-ready use).
- **PWA**: `manifest.json` and `sw.js` (Service Worker) for caching and mobile installation.

### 🚀 Installation and Usage

#### 1. Hosting (GitHub Pages)
This project is designed to be hosted for free on GitHub Pages:
1. The `index.html`, `manifest.json`, and `sw.js` files must be at the root of the repository.
2. Enable GitHub Pages under `Settings` > `Pages` > `main` branch.

#### 2. Mobile Installation (Turn it into an "App")
Once your GitHub Pages link is open:

**On Android (Chrome):**
1. Open the link in Chrome.
2. Tap the **three dots** (⋮) in the top right corner.
3. Select **"Add to Home screen"** or **"Install app"**.

**On iPhone (Safari):**
1. Open the link in Safari.
2. Tap the **Share** button (square with an arrow pointing up).
3. Scroll down and select **"Add to Home Screen"**.

### 📖 Quick Start Guide

1. **Initial Setup**: On first launch, enter your starting balance and your risk per trade as a percentage (e.g., 1% or 2%).
2. **Navigation**: Choose a month, then a week (the calendar follows a continuous 53-week-per-year format).
3. **Add a Trade**: Click an empty slot (maximum 8 per week).
4. **Entry**: Fill in the details. **Lot size** and **P&L** are calculated automatically as soon as you enter SL and TP. You can manually adjust the P&L if needed (slippage, partial exit).
5. **Save**: Click "Save". The overall balance updates instantly.

### ⚠️ IMPORTANT: Data Management

> **Critical note**: This app uses your browser's `localStorage`. This means your data is stored **locally on your device**.
> - If you clear your browser cache, you will lose your data.
> - **Best practice**: Regularly click the **"💾 Export JSON"** button and keep this file on your phone or email it to yourself.
> - To restore your data on a new device, use the **"Import JSON"** button.

### 📂 File Structure

```text
├── index.html       # Main structure and logic of the application
├── manifest.json    # PWA configuration (name, icon, theme)
├── sw.js            # Service Worker for caching and offline mode
└── README.md        # This documentation file
```

---

## 🇸🇴 Soomaali

Casharrad barnaamij PWA (Progressive Web App) oo heer sare ah, oo loogu talagalay ganacsatada doonaya inay si taxadar leh u kormeeraan waxqabadkooda, maamulaan halista, oo falanqeeyaan qaabdhismeedyadooda (setups).

Aplikeyshanku wuxuu shaqeeyaa **gabi ahaanba offline**, wuxuu ku rakibmaa taleefankaaga sida app dabiici ah (Android/iOS), wuxuuna isticmaalaa qaab-dhismeedka raadinta "doll-ka Ruushka" si loo helo habdhismeed ku habboon.

### ✨ Sifooyinka Muhiimka ah

- 📱 **100% Mobile & Offline**: Waxa lagu rakibi karaa shaashadda hore, wuxuuna shaqeeyaa iyada oo aan internet la haysan, mahad gelin Service Worker-ka.
- 🪆 **Raadinta "Doll-ka Ruushka"**: Dashboard → Bil → Usbuuc (si joogto ah 1 ilaa 53) → Ugu badnaan 8 trade usbuucba.
- 🧮 **Xisaabiye Caqli-gal ah**: Si toos ah ayuu u xisaabiyaa cabbirka lot-ka iyo P&L-ka dhabta ah, iyadoo lagu salaynayo balance-kaaga, halista (%) iyo isku-darka R:R (TP/SL).
- 📸 **Joornaal Muuqaal**: Waad ku dari kartaa sawirro "Ka hor" (setup) iyo "Ka dib" (natiijada) si toos ah oo ka socota sawir-gacmeedka taleefankaaga.
- 📈 **Tirakoob Wakhti-dhab ah**: Win Rate, tirada guulaha/khasaaraha, wadarta pips-ka TP/SL ee usbuuc kasta.
- 💾 **Kaydin La Qaadi Karo**: Soo dejin (export) iyo geli (import) dhammaan xogtaada qaabka JSON (kaydkaaga gaarka ah).
- 🎨 **Naqshad Heer Sare ah**: Muuqaal "Dark Mode" oo casri ah, nadiif ah, oo loo habeeyey ganacsiga.

### 🛠️ Tignoolajiyada La Isticmaalay

- **Frontend**: HTML5, CSS3 (Variables, Flexbox, Grid), Vanilla JavaScript (ma jiro framework culus).
- **Kaydinta**: Browser-ka `localStorage` (si loo isticmaalo isla markiiba, offline-na shaqeeya).
- **PWA**: `manifest.json` iyo `sw.js` (Service Worker) si loo kaydiyo cache-ka oo lagu rakibo mobile-ka.

### 🚀 Rakibidda iyo Isticmaalka

#### 1. Martigelinta (GitHub Pages)
Mashruucan waxa loogu talagalay in lagu martigeliyo bilaash GitHub Pages:
1. Faylasha `index.html`, `manifest.json` iyo `sw.js` waa inay ku jiraan saldhigga (root) ee repository-ga.
2. Daji GitHub Pages gudaha `Settings` > `Pages` > Laanta `main`.

#### 2. Rakibidda Mobile-ka (Si loo dhigo "App")
Marka linkiga GitHub Pages la furo:

**Android (Chrome):**
1. Linkiga ku fur Chrome.
2. Taabo **saddexda dhibic** (⋮) ee kor-midig.
3. Dooro **"Add to Home screen"** ama **"Install app"**.

**iPhone (Safari):**
1. Linkiga ku fur Safari.
2. Taabo badhanka **Share** (afar-gees leh fallaadh kor u jeedo).
3. Hoos u soco oo dooro **"Add to Home Screen"**.

### 📖 Hagaha Isticmaalka Degdega ah

1. **Habaynta Bilowga**: Markii aad markii hore furto, geli balance-kaaga bilowga iyo halistaada trade kasta boqolkiiba (tusaale: 1% ama 2%).
2. **Raadinta**: Dooro bil, ka dibna usbuuc (kalandarku wuxuu raacayaa qaab joogto ah oo 53 usbuuc sannadkii).
3. **Ku Dar Trade**: Riix meel madhan (ugu badnaan 8 usbuucba).
4. **Gelinta**: Buuxi faahfaahinta. **Lot-ka** iyo **P&L-ka** ayaa si toos ah loo xisaabiyaa isla markaad gelisid SL iyo TP. Waad ku beddeli kartaa P&L-ka gacanta haddii loo baahdo (slippage, ka bixid qayb ahaan).
5. **Kaydinta**: Riix "Save". Balance-ka guud ayaa isla markiiba cusboonaysiinaya.

### ⚠️ MUHIIM AH: Maamulka Xogta

> **Ogeysiis muhiim ah**: Aplikeyshankani wuxuu isticmaalaa `localStorage` ee browser-kaaga. Tani waxay ka dhigan tahay in xogtaadu lagu kaydiyo **gaarka ah qalabkaaga**.
> - Haddii aad nadiifiso cache-ka browser-kaaga, waxaad lumin doontaa xogtaada.
> - **Talo wanaagsan**: Si joogto ah u taabo badhanka **"💾 Export JSON"** oo ku haboo faylkan taleefankaaga ama u dir email ahaan.
> - Si aad xogtaada ugu soo celiso qalab cusub, isticmaal badhanka **"Import JSON"**.

### 📂 Qaab-dhismeedka Faylasha

```text
├── index.html       # Habdhismeedka iyo qaab-dhaqanka ugu weyn ee app-ka
├── manifest.json    # Habaynta PWA (magaca, sumadda, mowduuca)
├── sw.js            # Service Worker ee cache-ka iyo habka offline-ka
└── README.md        # Faylkan dukumeentiga
```
