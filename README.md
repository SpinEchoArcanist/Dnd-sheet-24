# Valeria Dawnbringer — Feuille de personnage D&D 5e

> **Paladin Aasimar · Malédiction de Strahd**  
> Fichier HTML unique, autonome, sans dépendance — conçu pour iPad via iOS Scriptable (WKWebView)

---

## Présentation

Ce projet est une feuille de personnage interactive pour **Donjons & Dragons 5e**, créée sur mesure pour le personnage **Valeria Dawnbringer** dans la campagne *Malédiction de Strahd*. Elle tourne entièrement dans un navigateur web ou dans l'application [Scriptable](https://scriptable.app/) sur iPad.

**Un seul fichier** — `dnd-sheet-v15.html` — contient l'intégralité du HTML, du CSS et du JavaScript. Aucune connexion serveur, aucune base de données, aucun framework.

---

## Démarrage rapide

1. Télécharger `dnd-sheet-v15.html`
2. L'ouvrir dans Safari, Chrome, ou tout navigateur moderne
3. Les données sont sauvegardées automatiquement dans le `localStorage` du navigateur (clé : `paladin_strahd_v3`)

### Sur iPad avec Scriptable

1. Copier le fichier dans iCloud Drive ou les Fichiers de Scriptable
2. Créer un script Scriptable qui charge le fichier via `WebView`
3. La feuille détecte automatiquement l'environnement WKWebView et s'adapte

---

## Fonctionnalités

### Identité du personnage

- **Nom, Classe, Espèce, Historique** — champs texte libres
- **Niveau** (1–20) — mis à jour en temps réel, recalcule toutes les statistiques dérivées
- **Bonus de Maîtrise** — calculé automatiquement selon le niveau
- La classe est verrouillée sur *Paladin* pour ce personnage

### Points de Vie

- **PV Max** — calculé automatiquement à partir du niveau, de la Constitution et des options ; modifiable manuellement ; bouton ↺ pour forcer le recalcul
- **Option Robuste** — ajoute +2 PV par niveau quand activée
- **Bonus PV externe** — pour les effets de sorts ou capacités temporaires
- **PV Actuels** — saisie directe ; couleur dynamique selon le niveau de vie :
  - 🟢 > 75 % — vert vif
  - 🟡 50–75 % — vert-jaune
  - 🟠 25–50 % — orange
  - 🔴 10–25 % — orange-rouge pulsant
  - ☠ < 10 % — rouge pulsant intense
- **PV Temporaires** — consommés en priorité avant les PV réels lors d'une blessure
- **Boutons Blessure / Soin** — appliquent les dégâts ou les soins directement sur les PV

### Sphère des Points de Vie

Visualisation animée en SVG : une sphère de cristal se remplit de rouge selon le niveau de vie. Inclut :

- Couche rouge pour les PV actuels
- Couche orange pour les PV temporaires
- Effets visuels : vapeur de sang, bulles, ombre pulsante, glow selon le seuil
- Affichage du score CA dans un bouclier héraldique gravé (change en or si *Bouclier de la Foi* est actif)

### Dés de Vie

- Type fixe : **d10** (Paladin)
- Maximum = niveau
- Boutons +/− pour les dépenser ou les récupérer
- Fiole animée affichant le ratio actuel/maximum
- Récupération au Repos Long : ⌈max/2⌉ dés restaurés

### Jets de Sauvegarde contre la Mort

Jauge horizontale accessible avec 6 segments tactiles (≥ 44 pt) :

- **3 segments Succès ♥** (vert) à gauche
- **3 segments Échecs ☠** (rouge) à droite
- Tap pour cocher/décocher chaque case
- État sauvegardé et restauré au rechargement

### Caractéristiques & Compétences

Six caractéristiques dans l'ordre d'affichage CON → FOR → CHA → DEX → SAG → INT :

- **Valeur brute** (éditable) → **Modificateur** (calculé automatiquement)
- **Sauvegarde** : case à cocher + valeur calculée incluant le bonus de maîtrise
- **Compétences** par caractéristique : case à cocher + valeur calculée
  - CON : aucune
  - FOR : Athlétisme
  - CHA : Intimidation, Persuasion, Tromperie, Représentation
  - DEX : Acrobaties, Discrétion, Escamotage, Adresse
  - SAG : Perception, Perspicacité, Médecine, Survie, Dressage
  - INT : Arcanes, Histoire, Investigation, Nature, Religion
- Les listes de compétences sont repliables/dépliables par caractéristique

### Combat

- **Initiative** = modificateur DEX (readonly)
- **Déplacement** en mètres (éditable, défaut 9 m)
- **Classe d'Armure** — calculée automatiquement depuis les armures équipées ; saisie manuelle possible ; Bonus CA externe disponible
- **CA + Bouclier** — affichée séparément si le sort *Bouclier de la Foi* est actif (+2)

### Aide aux Tests

Panneau de calcul rapide pour les jets en jeu :

- **Tests de Caractéristique** : sélectionner la carac ou la compétence, saisir le D20, le modificateur et le total s'affichent
- **Jets de Sauvegarde** : même principe, avec prise en charge de l'Aura de Protection (niveau 6)
- **Aura de Protection** : case à cocher — ajoute le modificateur de Charisme à tous les jets de sauvegarde si Valeria est niveau ≥ 6

### Attaque Rapide

Panneau dédié au combat, accessible en bas de page :

#### Sorts Actifs
Trois cases à cocher qui modifient les calculs en temps réel :
- **Arme Sacrée** — ajoute le modificateur de Charisme au toucher
- **Arme Magique** — ajoute +1 au toucher et aux dégâts
- **Bouclier de la Foi** — ajoute +2 à la CA

#### Initiative
Jet D20 + modificateur DEX = Total affiché

#### Attaque 1 & Attaque 2

Chaque bloc d'attaque comprend :

- **Sélecteur d'arme** — choisir parmi les armes de l'inventaire
- **Toggle Finesse** — FOR ou DEX si l'arme a la propriété Finesse
- **Quantité** — pour les armes consommables (flèches, carreaux, etc.)

**Toucher :**
- Saisie D20
- Modificateur de caractéristique (FOR ou DEX)
- Bonus de maîtrise
- Arme Sacrée (+MOD CHA) si active
- Arme Magique (+1) si active
- **Total calculé**

**Dégâts :**
- Saisie du résultat du dé (D4/D6/D8/D10 selon l'arme)
- Modificateur de caractéristique
- Arme Magique (+1) si active
- Type de dégâts (Radiant si Arme Sacrée)
- **Total calculé**

**Critique naturel (D20 = 20) :**
- Le champ D20 s'illumine en or avec une animation
- Le badge CRITIQUE ! apparaît
- L'indication de dés doublés s'affiche

#### Châtiment Divin / Fournaise

Pour chaque attaque, un bloc Châtiment optionnel :

- **Châtiment Divin** : 1 + niveau d'emplacement d8 (+ 1d8 contre Fiélon/Mort-vivant) de dégâts radiants
- **Châtiment de la Fournaise** : niveau d'emplacement d6 de dégâts de feu ; la cible effectue un jet de CON en début de tour
- En cas de critique, les dés sont automatiquement doublés
- Icônes de dés dynamiques selon le type et le niveau

#### Monture
- Modificateur d'attaque = FOR monture (+4) + MOD CHA du paladin
- Dégâts : 1d8 + niveau du sort (radiant/psychique/nécrotique selon le type)
- Critique pris en charge

#### Fin du Round
Bouton qui vide tous les champs D20 et dés de dégâts des 3 attaques, et remet à zéro les Châtiments.

### Magie

#### Caractéristique d'incantation & DD des sorts
Sélectionner la caractéristique (CHA pour un Paladin), le DD est calculé automatiquement : `8 + modificateur + maîtrise`

#### Emplacements de sorts
- **Conduit Divin** : max 2 (niv. 1–10) ou 3 (niv. 11+) — boutons +/− + fiole animée
- **Sort Niv. 1, 2, 3** : maximum calculé automatiquement selon le niveau, actuel modifiable — fioles animées
- Niveaux 4 et 5 prévus pour une future version

#### Imposition des Mains
- **PV Max** = 5 × niveau (calculé automatiquement)
- **PV Actuels** — saisie ou déduction via le panneau de soin
- **Main Guérisseuse Aasimar** — case à cocher (1×/repos long)
- Sphère de cristal animée avec couronne solaire dorée tournante, étoiles sacrées et bulles lumineuses
- Bouton ↺ pour restaurer au maximum

#### Monture d'Outremonde
Configuration de la monture invoquée :
- **Niveau du sort** (2–5)
- **Type** : Céleste, Fée ou Fielon
- CA, PV max, Dés de Vie — calculés automatiquement
- PV actuels persistés
- Table de statistiques fixe (FOR 18, DEX 12, CON 14, INT 6, SAG 12, CHA 8)
- Capacités spéciales affichées selon le type choisi :
  - *Céleste* — Contact guérisseur
  - *Fée* — Foulée féerique
  - *Fielon* — Regard fiélon
- Coup d'Outremonde et Lien Vital (communs à tous les types)
- PV restaurés au Repos Long

### Aptitudes, Traits et Dons

Trois catégories gérées via un formulaire overlay :

- **Traits d'espèce** (ex. Résistance céleste, Guérison des ténèbres)
- **Dons** — catégorisés : D'origine, Générale, Style de combat, Faveur épique
- **Aptitudes de classe** — avec niveau d'acquisition (1–20)

Chaque entrée peut avoir une description avec mise en forme gras/or. Clic sur le nom pour afficher la description. Tri automatique par catégorie et niveau.

### Inventaire

#### Objets
Ajout/modification/suppression d'objets libres avec nom et description.

#### Armes
Gestionnaire complet par arme :
- Caractéristique d'attaque (FOR / DEX)
- Dés de dégâts (D4 / D6 / D8 / D10), nombre de dés (1 ou 2)
- Types de dégâts (Acide, Contondant, Feu, Froid…)
- Portée (contact ou distance avec R1/R2)
- Propriétés (Finesse, Légère, Lourde, Polyvalente, etc.)
- Modificateurs d'attaque et de dégâts supplémentaires
- **Botte d'arme** (Enchaînement, Sap, Poussée, Renversement…) avec description
- Description libre
- **Arme consommable** — affiche un compteur de quantité dans l'inventaire et dans les blocs Attaque

Les armes sont disponibles dans le sélecteur des blocs Attaque 1 et 2.

#### Armures
Gestionnaire par armure :
- **Armure lourde** : CA fixe, Force minimale requise, désavantage Discrétion automatique
- **Armure légère** : base CA + MOD DEX
- **Armure intermédiaire** : base CA + min(MOD DEX, 2)
- **Bouclier** : +2 à la CA
- Bonus CA par armure
- Case Équipée / Déséquipée (une seule armure + un seul bouclier simultanément)

La CA est recalculée automatiquement quand une armure est équipée ou déséquipée. Un avertissement apparaît si *Discrétion* est sélectionnée dans l'Aide aux Tests et qu'une armure lourde est portée.

### Grimoire

Gestionnaire de sorts complet :

- **Compteur de préparation** : sorts préparés / maximum selon le niveau
- **Filtre** : afficher tous les sorts ou uniquement les sorts préparés
- **Tri** : par niveau croissant puis alphabétique
- **Groupes repliables** par niveau (Sorts mineurs, Niveau 1, 2…)
- Pour chaque sort :
  - Clic sur le nom → affiche/masque la description
  - **Préparé** — case à cocher (compte dans le maximum)
  - **Toujours prêt** — pour les sorts de Serment (ne compte pas dans le maximum)
  - Modifier (✏️) ou Supprimer (🗑️)
- Formulaire d'ajout/modification : Nom, Niveau (0–5), Description avec mise en forme

### Reliquaire

Panneau visuel en bas de page avec les ressources de combat :

| Élément | Description |
|---|---|
| Sphère PV | Visualisation animée des points de vie |
| Bouclier CA | Bouclier héraldique SVG avec la CA effective |
| Blessure / Soin | Saisie rapide pour appliquer des dégâts ou soins |
| Conduit Divin | Fiole or avec boutons +/− |
| Sort Niv. 1 / 2 / 3 | Fioles violet / bleu / vert avec boutons +/− |
| Dés de Vie | Fiole rouge avec boutons +/− |
| Sphère Imposition des Mains | Visualisation animée avec halo solaire |
| Soin par Imposition | Saisie et bouton ↺ restaurer |
| ☽ Repos Long | Restaure toutes les ressources |

### Repos Long

Le bouton ☽ Repos Long (avec confirmation) restaure :
1. PV actuels → PV max
2. PV temporaires → 0
3. Imposition des Mains → max
4. Conduit Divin → max
5. Main Guérisseuse Aasimar → décochée
6. Emplacements de sorts niv. 1, 2, 3 → max
7. Dés de Vie → +⌈max/2⌉ (plafonné au max)
8. PV de la Monture → max

---

## Effets Visuels

Le menu ⚙ propose un sous-menu *Effets visuels* pour activer/désactiver indépendamment :

- **Lueur pulsée** — halos animés sur les sphères et la couronne solaire
- **Effets sang (PV)** — vapeur de sang, veines, bulles dans la sphère PV
- **Poudre sacrée** — étoiles animées dans la sphère Imposition des Mains
- **Bulles** — bulles montantes dans les deux sphères
- **Lignes & reflets (fioles)** — animation de surface et reflet sur les fioles de ressources

Ces préférences ne sont pas persistées et reviennent à ON au rechargement.

---

## Sauvegarde & Transfert

### Sauvegarde automatique

Toutes les données sont sauvegardées dans le `localStorage` du navigateur après chaque modification. Clé : `paladin_strahd_v3`.

### Export JSON

Menu ⚙ → *Exporter* : affiche le JSON complet dans une zone de texte. Sélectionner tout et copier pour sauvegarder ou transférer.

### Import JSON

Menu ⚙ → *Importer* : coller un JSON précédemment exporté. La sanitisation valide et corrige automatiquement les données incomplètes ou d'un format ancien.

### Réinitialisation

Menu ⚙ → *Réinitialiser* (avec confirmation) : supprime le localStorage et recharge le personnage par défaut (Valeria Dawnbringer, niveau 5, CON 16, PV Max 59).

---

## Menus

| Action | Accès |
|---|---|
| Réinitialiser | ⚙ → Réinitialiser |
| Importer JSON | ⚙ → Importer |
| Exporter JSON | ⚙ → Exporter |
| Rafraîchir l'affichage | ⚙ → Rafraîchir |
| Tout replier | ⚙ → Tout replier |
| Tout déployer | ⚙ → Tout déployer |
| Effets visuels | ⚙ → Effets visuels |

---

## Architecture technique

```
dnd-sheet-v15.html
├── <head>
│   ├── Lien RPG Awesome 0.2.0 (icônes, CDN jsDelivr)
│   └── <style> — CSS inline complet
├── <body>
│   ├── En-tête + menu ⚙
│   ├── Grille 3 colonnes
│   │   ├── Colonne gauche  : Identité, Vie, Combat
│   │   ├── Colonne centrale: Caractéristiques & Compétences, Aide aux Tests
│   │   └── Colonne droite  : Magie, Inventaire
│   ├── Attaque Rapide (pleine largeur)
│   ├── Grimoire (pleine largeur)
│   ├── Reliquaire (pleine largeur — sphères + fioles)
│   ├── <template id="tpl-combat-block"> — template HTML des blocs Attaque
│   └── <script> — JavaScript inline complet
```

**Contraintes techniques respectées :**
- Zéro dépendance externe à l'exécution (hors 2 ressources CDN à chargement progressif)
- Compatible WKWebView iOS/iPadOS (Scriptable)
- `localStorage` avec `try/catch` obligatoire
- Tailles de police ≥ 14px sur tous les champs (évite le zoom automatique iOS)
- Animations SVG en SMIL uniquement (CSS animations sur SVG non fiables sur WKWebView)
- Cibles tactiles ≥ 44pt

---

## Dépendances (optionnelles, chargement progressif)

| Ressource | Usage | Fallback |
|---|---|---|
| [RPG Awesome 0.2.0](https://nagoshiashumari.github.io/Rpg-Awesome/) | Icônes (⚙ ⏱ ✏️ etc.) | Éléments vides, aucun texte perdu |
| [Metamorphous](https://fonts.google.com/specimen/Metamorphous) | Police gothique | Palatino Linotype → Georgia → serif |
| [game-icons.net](https://game-icons.net/) | Icônes SVG thématiques | Image vide invisible |

Si ces ressources sont indisponibles (mode hors-ligne, réseau restreint), la feuille reste entièrement fonctionnelle.

---

## Personnage par défaut

Au premier lancement ou après réinitialisation :

| Champ | Valeur |
|---|---|
| Nom | Valeria Dawnbringer |
| Classe | Paladin |
| Espèce | Aasimar |
| Historique | Fermier |
| Niveau | 5 |
| Robuste | Oui |
| PV Max | 59 |
| CON / FOR / CHA | 16 / 16 / 17 |
| DEX / SAG / INT | 12 / 11 / 10 |
| Armure | Cotte de mailles (CA 16) + Bouclier |
| Arme | Épée longue (d8, FOR, botte Sap) |
| Caractéristique d'incantation | Charisme |

---

## Versionnage

Le fichier suit un versionnage `MAJEUR.MINEUR` :

- **Mineur** : tout correctif, ajout ou modification → ex. 15.6 → 15.7
- **Majeur** : évolution structurelle significative validée explicitement → ex. 14.x → 15.0

La version courante est affichée discrètement en haut à droite de la feuille (`v15.7`).

---

## Licence

Ce projet est  sous licence open source MIT. Les ressources tierces (RPG Awesome, game-icons.net) sont soumises à leurs licences respectives (MIT / CC BY 3.0).

---

*Feuille de personnage développée itérativement — Malédiction de Strahd, D&D 5e*
