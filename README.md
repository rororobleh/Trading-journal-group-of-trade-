# 📊 Trading Journal Pro

🌐 **Langues / Languages / Luqadaha** : [🇫🇷 Français](#-trading-journal-pro) · [🇬🇧 English](#-trading-journal-pro-english) · [🇸🇴 Soomaali](#-trading-journal-pro-soomaali)

---

Application web **mono-fichier** (`index_2_.html`) de suivi de trading. Tout fonctionne hors-ligne, directement dans le navigateur, sans serveur ni installation : HTML, CSS et JavaScript sont contenus dans un seul fichier, et les données sont stockées localement via `localStorage`.

---

## 1. Vue d'ensemble

L'application permet de :

- créer une ou plusieurs **sessions** de trading (ex: un compte live, un compte de backtest, une année précise) ;
- enregistrer chaque trade avec sa paire, sa direction, son horaire, sa session de marché, son scénario de stratégie, son stop loss / take profit, son résultat et ses émotions ;
- imposer une **checklist de règles** propre à chaque scénario de stratégie (S1 à S4), à cocher entièrement avant de pouvoir enregistrer un trade ;
- **personnaliser ces règles** à tout moment (modifier, ajouter, supprimer, réinitialiser) ;
- visualiser des **statistiques globales** (win rate, P&L, courbe d'équité, répartition par paire / stratégie / session / émotion) ;
- naviguer les trades par **mois → semaine → trade** ;
- exporter/importer toutes les données en JSON pour sauvegarde ou transfert d'appareil.

Aucune donnée ne quitte l'appareil : tout est stocké dans le `localStorage` du navigateur.

---

## 2. Premier lancement — Écran de configuration

Au premier chargement (ou si aucune sauvegarde n'existe), l'écran **"Trading Journal Pro"** s'affiche et demande :

| Champ | Description |
|---|---|
| 🏷️ Nom de la session | Optionnel. Ex: "Backtest 2025", "Live Q1" |
| 📅 Année | Année de référence de la session |
| 💵 Balance initiale ($) | Capital de départ utilisé pour tous les calculs de risque |
| ⚠️ Risque par trade (%) | Pourcentage du capital risqué par trade (utilisé pour calculer automatiquement la taille de lot) |

Deux actions possibles :
- **Commencer →** : crée la session et ouvre l'application.
- **Restaurer une sauvegarde** : recharge les données précédemment enregistrées dans le `localStorage` (utile si l'écran de configuration apparaît alors que des données existent déjà, par exemple après un vidage de cache partiel).

---

## 3. Gestion des sessions

Une **session** représente un contexte de trading indépendant : son propre solde, son propre risque par trade, et ses propres semaines/trades.

### Créer une nouvelle session
Bouton **➕ Nouvelle Session** dans les Réglages (⚙️) → renvoie à l'écran de configuration initial pour créer une session supplémentaire sans perdre les données existantes (la session en cours est sauvegardée avant la bascule).

### Changer de session
Le sélecteur de session (icône session dans l'en-tête) ouvre une liste de toutes les sessions existantes, affichant pour chacune :
- l'année et le libellé,
- la balance actuelle,
- le P&L total cumulé (vert si positif, rouge si négatif),
- le risque par trade configuré,
- un badge **"Actif"** sur la session actuellement sélectionnée.

Cliquer sur une session bascule immédiatement l'application sur celle-ci.

### Modifier une session
Le panneau **⚙️ Réglages** permet de modifier à tout moment, pour la session active :
- le nom de la session,
- l'année,
- la balance actuelle,
- le risque par trade (%).

---

## 4. Navigation : Mois → Semaine → Trades

L'application organise les trades selon une hiérarchie à trois niveaux :

1. **Mois** : vue d'ensemble par mois de l'année de la session active.
2. **Semaine** : à l'intérieur d'un mois, les trades sont regroupés par semaine.
3. **Trades** : la liste des trades de la semaine sélectionnée, avec emplacements vides cliquables pour en ajouter de nouveaux.

Un fil d'Ariane (`Accueil › Mois › Semaine`) en haut de l'écran permet de revenir en arrière à tout moment.

---

## 5. Ajouter / modifier un trade

Cliquer sur un emplacement de trade (existant ou vide) ouvre une fenêtre modale avec les champs suivants :

### 5.1 Informations générales
| Champ | Détails |
|---|---|
| Paire | Sélection parmi les paires disponibles (ex: NAS100, US30, etc., avec icônes) |
| Direction | Achat / Vente |
| Date / Heure | Horodatage du trade |
| Session de marché | Londres, New York, Asie, Overlap |

### 5.2 Stratégie / Scénario — *cœur de la checklist de règles*

C'est ici qu'intervient le système de discipline de trading décrit en détail dans la **section 6**. Quatre boutons **S1 / S2 / S3 / S4** permettent de choisir le scénario utilisé pour ce trade. Le choix d'un scénario fait apparaître automatiquement sa checklist de règles associée.

Un lien **✏️ Gérer les règles**, situé juste au-dessus des boutons de scénario, ouvre l'éditeur de règles (section 7).

### 5.3 Calcul automatique du risque

Dès que le Stop Loss (SL) et le Take Profit (TP) sont saisis (en pips), l'application calcule en direct :

- **Montant risqué ($)** = Balance de la session × Risque par trade (%)
- **Taille de lot** = Montant risqué ÷ (SL × 10)
- **Ratio Risque/Récompense (R:R)** = TP ÷ SL
- **P&L estimé**, déterminé par le résultat sélectionné :
  - `WIN` → P&L = Montant risqué × R:R
  - `LOSS` → P&L = − Montant risqué
  - (Break-even ou autre statut → P&L = 0 sauf saisie manuelle)

Le champ P&L se met à jour automatiquement, mais reste un champ standard (modifiable si besoin).

### 5.4 Émotion, notes et captures d'écran
- **Émotion** : état émotionnel pendant le trade (utilisé ensuite dans les statistiques de répartition par émotion).
- **Notes** : commentaire libre.
- **Captures Avant / Après** : upload d'image (compressées et redimensionnées automatiquement côté client avant stockage, largeur max ~1000px, qualité JPEG 75%) pour illustrer le setup avant l'entrée et le résultat après la sortie.

### 5.5 Enregistrement

Le bouton **Enregistrer le trade** :
1. Vérifie qu'un scénario (S1–S4) est sélectionné — sinon affiche une alerte.
2. Vérifie que **toutes les règles de la checklist du scénario choisi sont cochées** — sinon affiche un avertissement visuel et empêche l'enregistrement (voir section 6.3).
3. Met à jour automatiquement la balance de la session en fonction du P&L du trade (en tenant compte de l'ancien P&L si c'est une modification).
4. Trie les trades de la semaine par date/heure.
5. Sauvegarde dans le `localStorage`.

Un bouton **Supprimer** (visible uniquement en modification d'un trade existant) permet de retirer le trade et d'ajuster la balance en conséquence.

---

## 6. Checklist de règles par scénario (S1–S4)

### 6.1 Principe

Chaque scénario de trading (S1, S2, S3, S4) est associé à une liste de règles à respecter, issues de la méthodologie de trading définie par l'utilisateur (zones de supply/demand, recherche de liquidity, breaks multi-timeframes, momentum, etc.).

Lorsqu'un scénario est sélectionné dans le formulaire de trade, sa checklist apparaît immédiatement sous les boutons S1–S4 :

- Chaque règle est affichée comme une ligne cliquable avec une case à cocher.
- Cliquer sur une ligne bascule son état (coché / décoché).
- Un compteur de progression (ex: `3/6`) indique le nombre de règles cochées sur le total, et passe en surbrillance verte une fois la checklist complète.

### 6.2 Règles par défaut

| Scénario | Règles par défaut |
|---|---|
| **S1** | Définir et confirmer le setup avant l'entrée (pas de scénario S2/S3/S4 applicable) |
| **S2** | Trend 15 min identifié · Supply/demand zone (pullback doit atteindre une zone, vérifiée sur plusieurs timeframes) · Recherche de liquidity (break 5 min) · Vérification d'une autre zone au niveau du break 1 min · Attente du break 1 min pour l'entry zone · TP fixé à la zone la plus proche (dernier HH/LL) |
| **S3** | Trend 15 min opposé au grand timeframe · Pullback 5 min · Attente que le pullback soit cassé · Zone déjà existante · Recherche de liquidity · Deuxième zone · Contre-trend break · Break 1 min · Attention au momentum |
| **S4** | 15 min LL/HH non cassé (condition d'éligibilité du scénario) · Trend 5 min / pullback 1 min (sans casser le 5 min) · Zone visible sur les grands timeframes · Liquidity sous le dernier HH/LL · Deuxième zone · Break 1 min |

Ces règles sont entièrement **personnalisables** (voir section 7) — le tableau ci-dessus représente uniquement les valeurs d'origine.

### 6.3 Blocage à l'enregistrement

Tant que toutes les règles du scénario sélectionné ne sont pas cochées, le bouton "Enregistrer le trade" :
- affiche un message d'avertissement (`⚠️ Coche toutes les règles avant d'enregistrer le trade.`) ;
- fait défiler automatiquement la vue jusqu'à la checklist ;
- n'enregistre rien.

Cela garantit qu'aucun trade ne soit journalisé sans validation explicite de la discipline de trading associée à son scénario.

### 6.4 Sauvegarde de l'état de checklist par trade

L'état des cases cochées au moment de l'enregistrement est sauvegardé avec le trade (`checklist: [true, true, false, ...]`). En réouvrant un trade existant pour le modifier :
- son scénario d'origine est automatiquement présélectionné ;
- sa checklist est restaurée (toutes les règles sont considérées validées par défaut si l'ancien trade n'a pas de checklist enregistrée, ou si le nombre de règles a changé depuis).

---

## 7. Éditeur de règles — Modifier, ajouter, supprimer des règles

### 7.1 Ouvrir l'éditeur

Le lien **✏️ Gérer les règles**, situé au-dessus des boutons S1–S4 dans le formulaire de trade, ouvre une fenêtre modale dédiée. Elle s'ouvre directement sur l'onglet du scénario actuellement sélectionné (ou S1 par défaut si aucun scénario n'est encore choisi).

### 7.2 Structure de l'éditeur

- **Onglets S1 / S2 / S3 / S4** : permettent de basculer entre les listes de règles de chaque scénario sans perdre les modifications en cours sur les autres onglets (chaque onglet édite une copie de travail indépendante).
- **Liste des règles** : chaque règle est affichée dans une zone de texte modifiable, avec un bouton **🗑️** pour la supprimer individuellement.
- **➕ Ajouter une règle** : ajoute un nouveau champ de texte vide en bas de la liste, prêt à être rempli (le focus se positionne automatiquement sur le nouveau champ).
- **Enregistrer les règles** : valide les modifications pour le scénario affiché. Les lignes vides ou ne contenant que des espaces sont automatiquement supprimées.
- **↺ Réinitialiser ce scénario aux règles par défaut** : restaure la liste d'origine du scénario affiché (avec confirmation), sans affecter les autres scénarios.

### 7.3 Comportement à l'enregistrement

Quand on clique sur **Enregistrer les règles** :
1. La liste nettoyée (sans lignes vides) remplace la liste existante pour ce scénario.
2. Les nouvelles règles sont sauvegardées dans le `localStorage` (clé `tj_scenario_rules_v1`), donc **persistantes** entre les sessions du navigateur.
3. Si le scénario modifié est celui actuellement sélectionné dans le formulaire de trade en cours, la checklist affichée se met à jour immédiatement :
   - les règles dont la position n'a pas changé conservent leur état coché/décoché précédent ;
   - les nouvelles règles ajoutées apparaissent décochées.

### 7.4 Portée des modifications

Les règles sont globales à l'application (et non propres à une session de trading) : elles s'appliquent à tous les futurs trades, quelle que soit la session active. Modifier les règles n'affecte pas la checklist déjà enregistrée sur les trades passés (chaque trade conserve l'état de checklist tel qu'il était au moment de son enregistrement).

---

## 8. Statistiques globales

Accessible via le bouton **📊 Stats** dans l'en-tête. Calculées sur l'ensemble des trades de la session active (tous mois/semaines confondus). Comprend :

- **Indicateurs clés** : nombre total de trades, win rate, P&L cumulé, etc.
- **Courbe d'équité** : évolution du solde au fil des trades.
- **Graphique mensuel** : performance par mois.
- **Donut des résultats** : répartition Win / Loss / Break-even.
- **Répartitions (breakdowns)** par :
  - paire de trading,
  - stratégie / scénario (S1–S4),
  - session de marché (Londres / New York / Asie / Overlap),
  - émotion ressentie pendant le trade.

---

## 9. Sauvegarde, export et import des données

### 9.1 Sauvegarde automatique
Chaque modification (ajout/édition/suppression de trade, changement de réglages, modification des règles) est immédiatement enregistrée dans le `localStorage` du navigateur sous la clé `tradingJournal_v2` (et `tj_scenario_rules_v1` pour les règles). Un indicateur **"Synchro"** apparaît brièvement dans l'en-tête à chaque sauvegarde réussie.

### 9.2 Export
Le bouton d'export génère un fichier JSON téléchargeable (`trading_backup_AAAA-MM-JJ.json`) contenant l'intégralité des sessions, semaines et trades.

### 9.3 Import
Le bouton d'import permet de recharger un fichier JSON exporté précédemment. Une confirmation est demandée car l'import **remplace toutes les données actuelles**. L'import reste compatible avec plusieurs anciens formats de données (structure par sessions, par années, ou structure simple à une seule session), pour faciliter la migration depuis des versions antérieures de l'application.

> ⚠️ Les règles de checklist personnalisées (section 7) ne font pas partie de l'export/import : elles sont stockées séparément (`tj_scenario_rules_v1`) et restent propres à l'appareil/navigateur utilisé.

---

## 10. Stockage et confidentialité

- **100% hors-ligne** : aucune donnée n'est envoyée vers un serveur. Tout est stocké localement via l'API `localStorage` du navigateur.
- **Clés de stockage utilisées** :
  - `tradingJournal_v2` : sessions, semaines, trades, balances, réglages de risque.
  - `tj_scenario_rules_v1` : règles personnalisées des checklists S1–S4.
- **Limites** : les données étant liées au navigateur et à l'appareil, vider le cache du navigateur ou changer d'appareil sans avoir exporté ses données entraîne leur perte. Il est recommandé d'exporter régulièrement une sauvegarde JSON (section 9.2).

---

## 11. Résumé technique

| Aspect | Détail |
|---|---|
| Fichier | `index_2_.html` — fichier unique autonome (HTML + CSS + JS) |
| Dépendances externes | Aucune (pas de framework, pas de CDN requis) |
| Stockage | `localStorage` du navigateur |
| Compatibilité | Tout navigateur moderne (desktop ou mobile) |
| Images | Compressées côté client en JPEG avant stockage en base64 |
| Graphiques | Dessinés via l'API Canvas native (pas de librairie de graphiques externe) |

---

## 12. Démarrage rapide

1. Ouvrir `index_2_.html` dans un navigateur.
2. Remplir l'écran de configuration initial (balance, risque, année).
3. Cliquer sur **Commencer →**.
4. Naviguer vers un mois, une semaine, puis cliquer sur un emplacement de trade vide.
5. Choisir un scénario (S1–S4), cocher chaque règle de la checklist au fur et à mesure de l'analyse du setup.
6. Remplir les informations du trade (paire, SL, TP, résultat, émotion...).
7. Cliquer sur **Enregistrer le trade**.
8. Consulter les statistiques globales via **📊 Stats**.
9. Exporter régulièrement une sauvegarde JSON pour ne pas perdre l'historique.

---
---

# 📊 Trading Journal Pro (English)

Single-file **web application** (`index_2_.html`) for trading journal tracking. Everything runs offline, directly in the browser, with no server and no installation: HTML, CSS, and JavaScript are all contained in one file, and data is stored locally via `localStorage`.

---

## 1. Overview

The application lets you:

- create one or more trading **sessions** (e.g. a live account, a backtest account, a specific year);
- log every trade with its pair, direction, time, market session, strategy scenario, stop loss / take profit, result, and emotions;
- enforce a **rules checklist** specific to each strategy scenario (S1 to S4), which must be fully checked before a trade can be saved;
- **customize these rules** at any time (edit, add, delete, reset);
- view **global statistics** (win rate, P&L, equity curve, breakdown by pair / strategy / session / emotion);
- navigate trades through a **month → week → trade** hierarchy;
- export/import all data as JSON for backup or device transfer.

No data ever leaves the device: everything is stored in the browser's `localStorage`.

---

## 2. First Launch — Setup Screen

On first load (or if no saved data exists), the **"Trading Journal Pro"** screen appears and asks for:

| Field | Description |
|---|---|
| 🏷️ Session name | Optional. E.g. "Backtest 2025", "Live Q1" |
| 📅 Year | Reference year for the session |
| 💵 Initial balance ($) | Starting capital used for all risk calculations |
| ⚠️ Risk per trade (%) | Percentage of capital risked per trade (used to automatically calculate lot size) |

Two possible actions:
- **Start →**: creates the session and opens the application.
- **Restore a backup**: reloads previously saved data from `localStorage` (useful if the setup screen appears even though data already exists, e.g. after a partial cache clear).

---

## 3. Session Management

A **session** represents an independent trading context: its own balance, its own risk per trade, and its own weeks/trades.

### Create a new session
**➕ New Session** button in Settings (⚙️) → returns to the initial setup screen to create an additional session without losing existing data (the current session is saved before switching).

### Switch session
The session selector (session icon in the header) opens a list of all existing sessions, showing for each one:
- the year and label,
- the current balance,
- the cumulative total P&L (green if positive, red if negative),
- the configured risk per trade,
- an **"Active"** badge on the currently selected session.

Clicking a session immediately switches the application to it.

### Edit a session
The **⚙️ Settings** panel allows you to modify, at any time, for the active session:
- the session name,
- the year,
- the current balance,
- the risk per trade (%).

---

## 4. Navigation: Month → Week → Trades

The application organizes trades in a three-level hierarchy:

1. **Month**: overview by month within the active session's year.
2. **Week**: within a month, trades are grouped by week.
3. **Trades**: the list of trades for the selected week, with clickable empty slots to add new ones.

A breadcrumb (`Home › Month › Week`) at the top of the screen lets you go back at any time.

---

## 5. Adding / Editing a Trade

Clicking on a trade slot (existing or empty) opens a modal window with the following fields:

### 5.1 General information
| Field | Details |
|---|---|
| Pair | Selection among available pairs (e.g. NAS100, US30, etc., with icons) |
| Direction | Buy / Sell |
| Date / Time | Trade timestamp |
| Market session | London, New York, Asia, Overlap |

### 5.2 Strategy / Scenario — *the heart of the rules checklist*

This is where the trading discipline system described in detail in **section 6** comes in. Four buttons **S1 / S2 / S3 / S4** let you choose the scenario used for this trade. Selecting a scenario automatically displays its associated rules checklist.

A **✏️ Manage rules** link, located just above the scenario buttons, opens the rules editor (section 7).

### 5.3 Automatic Risk Calculation

As soon as Stop Loss (SL) and Take Profit (TP) are entered (in pips), the application calculates in real time:

- **Risk amount ($)** = Session balance × Risk per trade (%)
- **Lot size** = Risk amount ÷ (SL × 10)
- **Risk/Reward ratio (R:R)** = TP ÷ SL
- **Estimated P&L**, determined by the selected result:
  - `WIN` → P&L = Risk amount × R:R
  - `LOSS` → P&L = − Risk amount
  - (Break-even or other status → P&L = 0 unless manually entered)

The P&L field updates automatically but remains a standard field (editable if needed).

### 5.4 Emotion, Notes, and Screenshots
- **Emotion**: emotional state during the trade (later used in emotion breakdown statistics).
- **Notes**: free-form comment.
- **Before / After screenshots**: image upload (automatically compressed and resized client-side before storage, max width ~1000px, JPEG quality 75%) to illustrate the setup before entry and the result after exit.

### 5.5 Saving

The **Save trade** button:
1. Checks that a scenario (S1–S4) is selected — otherwise shows an alert.
2. Checks that **all checklist rules for the chosen scenario are checked** — otherwise shows a visual warning and prevents saving (see section 6.3).
3. Automatically updates the session balance based on the trade's P&L (accounting for the previous P&L if editing).
4. Sorts the week's trades by date/time.
5. Saves to `localStorage`.

A **Delete** button (visible only when editing an existing trade) lets you remove the trade and adjust the balance accordingly.

---

## 6. Rules Checklist by Scenario (S1–S4)

### 6.1 Principle

Each trading scenario (S1, S2, S3, S4) is associated with a list of rules to follow, derived from the user-defined trading methodology (supply/demand zones, liquidity search, multi-timeframe breaks, momentum, etc.).

When a scenario is selected in the trade form, its checklist immediately appears below the S1–S4 buttons:

- Each rule is shown as a clickable line with a checkbox.
- Clicking a line toggles its state (checked/unchecked).
- A progress counter (e.g. `3/6`) shows how many rules are checked out of the total, and turns green once the checklist is complete.

### 6.2 Default Rules

| Scenario | Default rules |
|---|---|
| **S1** | Define and confirm the setup before entry (no S2/S3/S4 scenario applicable) |
| **S2** | 15 min trend identified · Supply/demand zone (pullback must reach a zone, verified across multiple timeframes) · Liquidity search (5 min break) · Verify another zone where the 1 min break occurred · Wait for the 1 min break for the entry zone · TP set at the nearest zone (last HH/LL) |
| **S3** | 15 min trend opposite to the higher timeframe · 5 min pullback · Wait for the pullback to be broken · Already existing zone · Liquidity search · Second zone · Counter-trend break · 1 min break · Watch the momentum |
| **S4** | 15 min LL/HH not broken (eligibility condition for the scenario) · 5 min trend / 1 min pullback (without breaking the 5 min) · Zone visible on higher timeframes · Liquidity below the last HH/LL · Second zone · 1 min break |

These rules are fully **customizable** (see section 7) — the table above represents only the original default values.

### 6.3 Save Blocking

As long as not all rules for the selected scenario are checked, the "Save trade" button:
- displays a warning message (`⚠️ Check all the rules before saving the trade.`);
- automatically scrolls the view to the checklist;
- saves nothing.

This ensures no trade is logged without explicit validation of the trading discipline associated with its scenario.

### 6.4 Per-Trade Checklist State Storage

The state of checked boxes at the time of saving is stored with the trade (`checklist: [true, true, false, ...]`). When reopening an existing trade to edit it:
- its original scenario is automatically pre-selected;
- its checklist is restored (all rules are considered validated by default if the old trade has no stored checklist, or if the number of rules has changed since then).

---

## 7. Rules Editor — Edit, Add, Delete Rules

### 7.1 Opening the Editor

The **✏️ Manage rules** link, located above the S1–S4 buttons in the trade form, opens a dedicated modal window. It opens directly on the tab of the currently selected scenario (or S1 by default if no scenario is selected yet).

### 7.2 Editor Structure

- **S1 / S2 / S3 / S4 tabs**: let you switch between each scenario's rule lists without losing in-progress edits on other tabs (each tab edits an independent working copy).
- **Rules list**: each rule is displayed in an editable text area, with a **🗑️** button to delete it individually.
- **➕ Add a rule**: adds a new empty text field at the bottom of the list, ready to be filled in (focus automatically moves to the new field).
- **Save rules**: confirms the changes for the displayed scenario. Empty or whitespace-only lines are automatically removed.
- **↺ Reset this scenario to default rules**: restores the original list for the displayed scenario (with confirmation), without affecting other scenarios.

### 7.3 Save Behavior

When clicking **Save rules**:
1. The cleaned list (without empty lines) replaces the existing list for that scenario.
2. The new rules are saved to `localStorage` (key `tj_scenario_rules_v1`), making them **persistent** across browser sessions.
3. If the edited scenario is the one currently selected in the active trade form, the displayed checklist updates immediately:
   - rules whose position hasn't changed keep their previous checked/unchecked state;
   - newly added rules appear unchecked.

### 7.4 Scope of Changes

Rules are global to the application (not specific to a trading session): they apply to all future trades, regardless of the active session. Editing rules does not affect the checklist already saved on past trades (each trade keeps the checklist state as it was at the time it was saved).

---

## 8. Global Statistics

Accessible via the **📊 Stats** button in the header. Calculated across all trades in the active session (all months/weeks combined). Includes:

- **Key indicators**: total number of trades, win rate, cumulative P&L, etc.
- **Equity curve**: balance evolution over the trades.
- **Monthly chart**: performance by month.
- **Results donut**: Win / Loss / Break-even breakdown.
- **Breakdowns** by:
  - trading pair,
  - strategy / scenario (S1–S4),
  - market session (London / New York / Asia / Overlap),
  - emotion felt during the trade.

---

## 9. Saving, Exporting, and Importing Data

### 9.1 Automatic Save
Every change (adding/editing/deleting a trade, changing settings, editing rules) is immediately saved to the browser's `localStorage` under the key `tradingJournal_v2` (and `tj_scenario_rules_v1` for rules). A **"Synced"** indicator briefly appears in the header on each successful save.

### 9.2 Export
The export button generates a downloadable JSON file (`trading_backup_YYYY-MM-DD.json`) containing all sessions, weeks, and trades.

### 9.3 Import
The import button allows reloading a previously exported JSON file. A confirmation is requested because importing **replaces all current data**. Import remains compatible with several older data formats (session-based structure, year-based structure, or simple single-session structure), to ease migration from earlier versions of the application.

> ⚠️ Custom checklist rules (section 7) are not part of export/import: they are stored separately (`tj_scenario_rules_v1`) and remain specific to the device/browser used.

---

## 10. Storage and Privacy

- **100% offline**: no data is ever sent to a server. Everything is stored locally via the browser's `localStorage` API.
- **Storage keys used**:
  - `tradingJournal_v2`: sessions, weeks, trades, balances, risk settings.
  - `tj_scenario_rules_v1`: custom rules for S1–S4 checklists.
- **Limitations**: since data is tied to the browser and device, clearing the browser cache or switching devices without exporting data first will result in data loss. It is recommended to regularly export a JSON backup (section 9.2).

---

## 11. Technical Summary

| Aspect | Detail |
|---|---|
| File | `index_2_.html` — single self-contained file (HTML + CSS + JS) |
| External dependencies | None (no framework, no CDN required) |
| Storage | Browser `localStorage` |
| Compatibility | Any modern browser (desktop or mobile) |
| Images | Client-side compressed to JPEG before being stored as base64 |
| Charts | Drawn using the native Canvas API (no external charting library) |

---

## 12. Quick Start

1. Open `index_2_.html` in a browser.
2. Fill in the initial setup screen (balance, risk, year).
3. Click **Start →**.
4. Navigate to a month, a week, then click on an empty trade slot.
5. Choose a scenario (S1–S4), check each checklist rule as you analyze the setup.
6. Fill in the trade details (pair, SL, TP, result, emotion...).
7. Click **Save trade**.
8. Check global statistics via **📊 Stats**.
9. Regularly export a JSON backup to avoid losing your history.

---
---

# 📊 Trading Journal Pro (Soomaali)

**Codsiga websaydhka** ee hal-faylka ah (`index_2_.html`) loogu talagalay raadraaca ganacsiga trading-ka. Wax kastaa waxay shaqeeyaan xaalad offline ah, toos browser-ka gudihiisa, adoon u baahnayn server ama rakibid: HTML, CSS iyo JavaScript waxaa lagu ururiyey hal fayl, xogtana waxaa lagu keydinayaa maxalliga ah `localStorage` iyada.

---

## 1. Guud ahaan

Codsigani wuxuu kuu oggolaanayaa inaad:

- abuuro mid ama dhowr **session** oo ganacsiga trading ah (tusaale: xisaab toos ah, xisaab backtestka, sanad gaar ah);
- diiwaan geli ganacsiga kasta oo leh lambarkeeda, jihada, wakhtiga, session-ka suuqa, xaaladda xeeladda, stop loss / take profit, natiijada iyo dareenka;
- ku khasbid **liiska xeerarka** gaar u ah xaaladda xeelad kasta (S1 ilaa S4), kaas oo dhami in la xaqiijiyo ka hor inta aan ganacsi la keydin;
- **ku habeyn xeerarkaan** waqti kasta (wax ka bedel, kudar, tirtir, dib u deji);
- eeg **xogta guud** (xadka guusha, P&L, khadka hantida, kala-qaybsanaanta lambarada / xeeladda / session-ka / dareenka);
- u socodsii ganacsiga sida **bilood → toddobaad → ganacsi**;
- dhoofin/soo dejin dhammaan xogta JSON ahaan si loo kaydio ama loo wareejiyo qalabka kale.

Xog ma gaadho server: wax kastaa waxaa lagu keydinayaa `localStorage` browser-ka.

---

## 2. Bilowga Koowaad — Shaashadda Habeynta

Markii codsiga la furo marka ugu horeysa (ama haddaan kaydinta jirin), shaashadda **"Trading Journal Pro"** ayaa soo baxa waxayna weyddiisaa:

| Beer | Sharaxaad |
|---|---|
| 🏷️ Magaca session-ka | Ikhtiyaari. Tusaale: "Backtest 2025", "Live Q1" |
| 📅 Sanadka | Sanadka tixraaca session-ka |
| 💵 Dheefshiidka bilowga ($) | Maalgashiga la bilaabayo oo loo isticmaalo xisaabinta khatarta oo dhan |
| ⚠️ Khatarta ganacsiga kasta (%) | Boqolkiimaha maalgashiga la khatareeyo ganacsi kasta (waxaa loo isticmaalaa si toos ah u xisaabinta cabbirka lot) |

Labada falaleed ee suurtogalka ah:
- **Bilow →**: waxay abuurtaa session-ka oo furaysaa codsiga.
- **Soo celib kaydinta**: waxay dib u soo dejinaysaa xogta hore ee lagu keydinay `localStorage` (waxay ku waxtar tahay haddii shaashadda habeyntu soo baxdo xitaa haddii xog jirto, tusaale ka dib nadiifinta cache-ka qayb ahaan).

---

## 3. Maaraynta Session-ka

**Session** waxay u taabantaa macne ganacsiga madaxbannaan: dheefshiidkeeda, khataraheedda ganacsi kasta, iyo toddobaadadeeda/ganacsigeedaba.

### Abuurista session cusub
Badhanka **➕ Session Cusub** Goobta Dejinta (⚙️) → waxay ku celisaa shaashadda habeynta bilowga si loo abuuro session dheeraad ah iyada oo la waaysan xogta jirta (session-ka hadda jirta waxaa lagu keydinayaa ka hor is-bedelka).

### Baddelida session
Doortaha session-ka (astaan session ah madaxa codsiga) wuxuu furaa liiska dhammaan session-yada jira, oo muujinaya mid kasta:
- sanadka iyo cinwaanka,
- dheefshiidka hadda,
- wadarta P&L joogtada ah (cagaaran haddii togan yahay, casaan haddii taban yahay),
- khatarta ganacsi kasta ee loo habeeyay,
- calaamad **"Firfircoon"** oo ku taal session-ka hadda la dooratay.

Gujinta session-ka waxay si dhakhso ah u beddeshaa codsiga session-kaas.

### Tafatirka session
Panelka **⚙️ Dejinta** wuxuu kuu oggolaanayaa inaad wax ka beddesho, waqti kasta, session-ka firfircoon:
- magaca session-ka,
- sanadka,
- dheefshiidka hadda,
- khatarta ganacsi kasta (%).

---

## 4. Socodsiinta: Bilood → Toddobaad → Ganacsiga

Codsigani wuxuu u habeeyaa ganacsiga sida heerarka saddex-daran:

1. **Bilood**: muuqaal guud bilood kasta ee sanadka session-ka firfircoon.
2. **Toddobaad**: gudaha bilood, ganacsiga waxaa lagu koobyaa toddobaad kasta.
3. **Ganacsiga**: liiska ganacsiga toddobaadka la doortay, oo leh meel bannaan oo la gujin karo si cusub loo daro.

Jihaynta (`Guriga › Bilood › Toddobaad`) oo ku taal sare shaashadda waxay kuu oggolaanaysaa inaad dib u laabatid waqti kasta.

---

## 5. Ku Darka / Tafatirka Ganacsi

Gujinta meel ganacsi ah (jirta ama bannaan) waxay furaysaa daaqadda qaab-dhismeedka oo leh meelaha soo socda:

### 5.1 Macluumaadka guud
| Beer | Faahfaahin |
|---|---|
| Labada | Doorasho ka mid ah labadaha la heli karo (tusaale: NAS100, US30, iwm., astaamaha leh) |
| Jihada | Iibso / Iib |
| Taariikhda / Wakhtiga | Wakhtiga ganacsigu dhacdey |
| Session-ka suuqa | London, New York, Aasiya, Overlap |

### 5.2 Xeeladda / Xaaladda — *wadnaha liiska xeerarka*

Kani waa meesha ay ka timid nidaamka hagista ganacsiga oo lagu sharxay si faahfaahsan **qeybta 6**. Afarta badhanka **S1 / S2 / S3 / S4** waxay kuu oggolaanayaan inaad doorato xaaladda la isticmaalo ganacsigas. Doorashada xaaladda waxay si toos ah u muujinaysaa liiska xeerarkiisa.

Xiriirka **✏️ Maamul xeerarka**, oo ku yaal sare badhannada xaaladda, wuxuu furaa tafatiraha xeerarka (qeybta 7).

### 5.3 Xisaabinta Khatarta si Toos ah

Markii Stop Loss (SL) iyo Take Profit (TP) la galiyo (pips-yada), codsigani wuxuu xisaabiyaa si toos ah:

- **Lacagta la khatareeyo ($)** = Dheefshiidka session-ka × Khatarta ganacsi kasta (%)
- **Cabbirka lot** = Lacagta la khatareeyo ÷ (SL × 10)
- **Saamiga Khatar/Abaalmarinta (R:R)** = TP ÷ SL
- **P&L la filayo**, oo go'doomiya natiijada la dooratay:
  - `WIN` → P&L = Lacagta la khatareeyo × R:R
  - `LOSS` → P&L = − Lacagta la khatareeyo
  - (Break-even ama xaaladda kale → P&L = 0 haddaan gacanta lagu gelin)

Beerta P&L waxay si toos ah u cusboonaanaysaa, laakiin waxay ahaataa beer caadi ah (la wax ka bedeli karo haddii loo baahdo).

### 5.4 Dareenka, Xusuustaasha iyo Sawirrada

- **Dareenka**: xaaladda dareenka intii lagu guda jiray ganacsigu (ka dib waxaa loo isticmaalaa xogta kala-qaybsanaanta dareenka).
- **Xusuustaasha**: faallo xor ah.
- **Sawirrada Ka Hor / Ka Dib**: gal sawir (oo si toos ah loo caddeeyay oo loo yareeyay dhinaca macmiilka ka hor kaydinta, ballaca ugu badan ~1000px, tayada JPEG 75%) si loo muujiyo dejinta ka hor gelitaanka iyo natiijada ka dib bixitaanka.

### 5.5 Keydintu

Badhanka **Keydi ganacsigu**:
1. Xaqiijiyaa in xaalad (S1–S4) la doortay — haddaan la dooranin wuxuu muujiyaa digniinta.
2. Xaqiijiyaa in **dhammaan xeerarka liiska xaaladda la doortay la saxiixay** — haddaan la saxiixin wuxuu muujiyaa digniin aragga ah oo xukumaya kaydintu (arag qeybta 6.3).
3. Si toos ah u cusboonaynta dheefshiidka session-ka iyadoo lagu saleynayo P&L ganacsigu (iyada oo la tixgelinayo P&L hore haddii la tafatirayo).
4. Kala soocida ganacsiga toddobaadka ah taariikhda/wakhtiga.
5. Keydintu `localStorage` ku jira.

Badhanka **Tirtir** (oo muuqda oo kaliya marka la tafatirayo ganacsi jira) waxay kuu oggolaanaysaa inaad saarto ganacsigu oo aad si waafaqsan u dejiso dheefshiidka.

---

## 6. Liiska Xeerarka Xaaladda (S1–S4)

### 6.1 Mabda'a

Xaaladda ganacsiga kasta (S1, S2, S3, S4) waxaa lala xidhiiyay liis xeerarka la raacayo, kuwaas oo ka soo jeedda qaababka ganacsiga ay isticmaalayaan isticmaalayaasha (goobaha supply/demand, raadinta biyaha, jabinta multi-timeframe, momentum, iwm.).

Markii xaalad la dooranayo qaab-dhismeedka ganacsigu, liisteedu si toos ah ayey u soo muuqataa hoose badhannada S1–S4:

- Xeer kasta waxaa lagu muujiyaa saf la gujin karo oo leh sanduuq saxiixid.
- Gujinta saf waxay beddelaysaa xaaladdiisa (saxiixay / la saxiixin).
- Tirinta horumarinta (tusaale: `3/6`) waxay muujinaysaa tirada xeerarka la saxiixay wadarta ka mid ah, oo cagaaran noqota marka liiska dhammaado.

### 6.2 Xeerarka Caadiga ah

| Xaaladda | Xeerarka Caadiga ah |
|---|---|
| **S1** | Qeex oo xaqiiji dejinta ka hor gelitaanka (xaalad S2/S3/S4 ma khuseyso) |
| **S2** | Trend 15 daqiiqo la gartay · Goobta supply/demand (pullback waa inuu gaara goor, oo lagu xaqiijiyay dhowr timeframe) · Raadinta biyaha (jabinta 5 daqiiqo) · Xaqiijinta goor kale meesha jabinta 1 daqiiqo dhacdey · Sugista jabinta 1 daqiiqo ee goorta gelitaanka · TP lagu dejiyay goobta ugu dhow (HH/LL ugu dambeeyay) |
| **S3** | Trend 15 daqiiqo ka soo horjeedda timeframe-ka weyn · Pullback 5 daqiiqo · Sugista in pullback-ku jabo · Goor horay u jiray · Raadinta biyaha · Goorta labaad · Jabinta ka-soo-horjeedda trend-ka · Jabinta 1 daqiiqo · Feejignaan momentum-ka |
| **S4** | LL/HH 15 daqiiqo aan jabnayn (shuruudda xaaladda u qalmid) · Trend 5 daqiiqo / pullback 1 daqiiqo (adoon jabinnayn 5 daqiiqo) · Goor muuqata timeframe-yada weyn · Biyaha hoose HH/LL ugu dambeeyay · Goorta labaad · Jabinta 1 daqiiqo |

Xeerarkaan waxaa si buuxda **loo habeyn karaa** (arag qeybta 7) — shaxda kore waxay u taabantaa oo kaliya qiyamka asalka ah.

### 6.3 Xukumida Keydintu

Muddo dhammaan xeerarka xaaladda la doortay aan la saxiixin, badhanka "Keydi ganacsigu":
- wuxuu muujiyaa farriin digniin (`⚠️ Saxiix dhammaan xeerarka ka hor inta aadan keydin ganacsigu.`);
- si toos ah u duulidda muuqaalka liistaha;
- wax ma keydiyo.

Tani waxay hubinaysaa in ganacsi aan la diiwaangelin iyada oon si cad u xaqiijinin xeeladdii ganacsiga ee lala xidhiiyay xaaladdiisa.

### 6.4 Keydintu Xaaladda Liiska Ganacsi kasta

Xaaladda sanduuqyada la saxiixay waqtiga kaydintu waxaa lagu keydinayaa ganacsigu (`checklist: [true, true, false, ...]`). Marka dib loo furay ganacsi jira si loo tafatiro:
- xaaladdiisa asalka ah waxaa si toos ah loo doortaa;
- liiskiisa waxaa dib loo soo celiyaa (dhammaan xeerarka waxaa loo tixgeliyaa ansaxsan si caadi ahaan haddii ganacsigu hore u haysan liis kaydsan, ama haddii tirada xeerarka ay is beddesheen tan iyo).

---

## 7. Tafatiraha Xeerarka — Wax ka bedel, Kudar, Tirtir Xeerarka

### 7.1 Furista Tafatiraha

Xiriirka **✏️ Maamul xeerarka**, oo ku yaal sare badhannada S1–S4 qaab-dhismeedka ganacsigu, wuxuu furaa daaqad gaar ah. Waxay si toos ah ugu furaysaa tabka xaaladda hadda la doortay (ama S1 si caadi ahaan haddaan xaaladna la dooranin weli).

### 7.2 Qaab-dhismeedka Tafatiraha

- **Tabmada S1 / S2 / S3 / S4**: waxay kuu oggolaanayaan inaad u wareejid liisaska xeerarka xaaladda kasta iyada oon la waaysan wax ka bedelyada dhexdooda ee tabmadaha kale (tab kasta wuxuu tafatiraa nuqulka shaqo madaxbannaan).
- **Liiska xeerarka**: xeer kasta waxaa lagu muujiyaa goob qoraal la tafatiri karo, oo leh badhanka **🗑️** si gaar ahaan loo tirtiro.
- **➕ Kudar xeer**: wuxuu ku daraa beer qoraal cusub oo madhan xagga hoose ee liiska, diyaar in la buuxiyo (fekerku si toos ah ayuu ugu socdaa beerta cusub).
- **Keydi xeerarka**: wuxuu xaqiijiyaa wax ka bedelyada xaaladda la muujinayo. Safadaha madhan ama kuwa kaliya meel bannaan ka kooban waxaa si toos ah laga saartaa.
- **↺ Dib u deji xaaladdan xeerarkii caadiga ahayd**: waxay soo celisaa liistii asalka ahayd xaaladda la muujinayo (oo leh xaqiijin), iyada oon saameyn xaaladaha kale.

### 7.3 Dhaqanka Marka La Keydiyay

Marka la gujiyo **Keydi xeerarka**:
1. Liiska la nadiifeeyay (aan lahayn safadaha madhan) wuxuu beddelaa liiska jira xaaladda.
2. Xeerarka cusub waxaa lagu keydinayaa `localStorage` (furaha `tj_scenario_rules_v1`), taas oo ka dhigaysa **joogta ah** inta lagu jiro session-yada browser-ka.
3. Haddii xaaladda la tafatiroo ay tahay ta hadda la doortay qaab-dhismeedka ganacsigu firfircoon, liiska la muujinayo wuxuu si toos ah u cusboonaanayaa:
   - xeerarka meesha uusan is beddelin waxay haystaan xaaladoodii hore ee saxiixay/la saxiixin;
   - xeerarka cusub ee la daray waxay si cad u muuqdaan.

### 7.4 Xudduudka Wax Ka Bedelyada

Xeerarka waxaa u guud codsiga (mana gaarka ahayn session-ka ganacsiga): waxay ku dhaqmaan dhammaan ganacsiga mustaqbalka, xaaladda firfircoon waa ayaan kala sooc lahayn. Bedelida xeerarka kama saameyn liistaha horay lagu keydinay ganacsiga hore (ganacsi kasta wuxuu ilaaliyaa xaaladda liistaha sida ay ahayd waqtiga loo keydinayey).

---

## 8. Xogta Guud

Waxaa la gaari karaa badhanka **📊 Xogta** madaxa codsiga. Waxaa lagu xisaabiyaa dhammaan ganacsiga session-ka firfircoon (dhammaan biloodaha/toddobaadaha la xidid). Waxaa ku jira:

- **Tilmaamaha muhiimka ah**: tirada ganacsiga oo dhan, xadka guusha, P&L joogtada ah, iwm.
- **Khadka hantida**: isbeddellada dheefshiidka ganacsiga oo dhan.
- **Shaxda bishii**: waxqabadka bil kasta.
- **Donut natiijada**: kala-qaybsanaanta Win / Loss / Break-even.
- **Kala-qaybsanaantu** by:
  - lambarada ganacsiga,
  - xeeladda / xaaladda (S1–S4),
  - session-ka suuqa (London / New York / Aasiya / Overlap),
  - dareenka la dareemay intii lagu jiray ganacsigu.

---

## 9. Keydintu, Dhoofinta iyo Soo Dejinta Xogta

### 9.1 Keydintu si Toos ah
Isbeddel kasta (darista/tafatirka/tirtiridda ganacsi, bedelida dejimaha, bedelida xeerarka) si toos ayaa loogu keydinayaa `localStorage` browser-ka furaha `tradingJournal_v2` (iyo `tj_scenario_rules_v1` xeerarka). Tilmaan **"La Waafajiyay"** ayaa si xoog ah uga soo muuqata madaxa keydinta guul kasta ka dib.

### 9.2 Dhoofinta
Badhanka dhoofinta wuxuu dhaliyaa fayl JSON oo la soo dejin karo (`trading_backup_SSSS-BB-MM.json`) oo ku jira dhammaan session-yada, toddobaadyada iyo ganacsiga.

### 9.3 Soo Dejinta
Badhanka soo dejinta wuxuu kuu oggolaanayaa inaad dib u shidid fayl JSON hore loo dhoofiyay. Xaqiijin ayaa la codsanayaa sababtoo ah soo dejintu **waxay beddelaysaa dhammaan xogta hadda jirta**. Soo dejintu waxay ku waafaqsantahay dhowr qaab-dhismeed oo xog-kaydis oo hore (qaab-dhismeedka session-yada, qaab-dhismeedka sanadyada, ama qaab-dhismeedka fudud ee hal session), si loo fududeeyo u wareejimida ka noocyadii hore ee codsiga.

> ⚠️ Xeerarka liiska gaar u ah (qeybta 7) kuma jiraan dhoofinta/soo dejinta: waxaa lagu keydinayaa gooni (`tj_scenario_rules_v1`) waxayna ahaadaan gaarka ah qalabka/browser-ka la isticmaalayo.

---

## 10. Kaydinta iyo Xogta Gaarka ah

- **100% offline**: xog ma dirin server. Wax kastaa waxaa lagu keydinayaa maxalliga ah `localStorage` API browser-ka.
- **Furahaaha kaydinta la isticmaalo**:
  - `tradingJournal_v2`: session-yada, toddobaadyada, ganacsiga, dheefshiidyada, dejimaha khatarta.
  - `tj_scenario_rules_v1`: xeerarka gaar u ah liisaska S1–S4.
- **Xudduudka**: xogtu xidnaatahay browser-ka iyo qalabka, nadiifinta cache-ka browser-ka ama baddelida qalabka iyada oon xogta la dhoofin ayaa keeni doona lumista xogta. Waxaa lagula talinayaa inaad si joogto ah u dhoofiso kaydinta JSON (qeybta 9.2).

---

## 11. Koobitaanka Farsamada

| Dhinac | Faahfaahin |
|---|---|
| Faylka | `index_2_.html` — hal fayl madaxbannaane ah (HTML + CSS + JS) |
| Ku-tiirso dibadda | Midna ma jiro (framework ma jiro, CDN ma loo baahna) |
| Kaydinta | `localStorage` browser-ka |
| Waafajnaanta | Browser casri kasta (desktop ama mobile) |
| Sawirrada | Dhinaca macmiilka loogu caddeeyay JPEG ka hor inta la kaydiyaan base64 |
| Shaxadaha | Lagu sawiraa API Canvas-ka asalka ah (ma jiro maktabad shax dibadeed ah) |

---

## 12. Bilaabista Degdegga ah

1. Fur `index_2_.html` browser-ka.
2. Buuxi shaashadda habeynta bilowga (dheefshiid, khatar, sanad).
3. Guji **Bilow →**.
4. U socodsii bilood, toddobaad, ka dibna guji meel ganacsi madhan.
5. Dooro xaalad (S1–S4), saxiix xeer kasta oo liistaha intaad u falanqeyneyso dejinta.
6. Buuxi macluumaadka ganacsigu (lambarka, SL, TP, natiijada, dareenka...).
7. Guji **Keydi ganacsigu**.
8. Hubi xogta guud **📊 Xogta** iyada.
9. Si joogto ah u dhoofiso kaydinta JSON si aadan u waaysan taariikhda.

