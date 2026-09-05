# Modifications à apporter au mémoire
*Date : 5 septembre 2026*

Ce document recense toutes les modifications à effectuer suite aux remarques de la tutrice pédagogique.

---

## 1. ENRICHISSEMENT EMPIRIQUE DU VOLET PRÉDICTIF

### Remarque
> Intégrer un tableau récapitulatif des métriques de performance ($R^2$, MAE, RMSE) sur données réelles pour valider les modèles XGBoost et Random Forest du Chapitre 4 (ou expliciter les contraintes d'accès aux données en tant que limite si ce test n'a pu être finalisé).

### Localisation
- **Fichier** : `sections/modelisation.tex`
- **Section concernée** : §4.2 ou §4.3 (modèles prédictifs)

### Modifications à effectuer

#### Option A : Si les tests ont été réalisés
Ajouter un tableau récapitulatif après la présentation des modèles XGBoost et Random Forest :

```latex
\begin{table}[htbp]
\centering
\caption{Performance des modèles prédictifs sur données réelles}
\label{tab:metriques-performance}
\begin{tabular}{lccc}
\toprule
\textbf{Modèle} & \textbf{$R^2$} & \textbf{MAE (min)} & \textbf{RMSE (min)} \\
\midrule
Random Forest   & 0.XX & XX.X & XX.X \\
XGBoost        & 0.XX & XX.X & XX.X \\
\bottomrule
\end{tabular}
\end{table}
```

Accompagner le tableau d'un paragraphe d'analyse :
- Comparer les performances des deux modèles
- Commenter le $R^2$ : quelle part de la variance est expliquée ?
- Interpréter MAE et RMSE : précision en minutes
- Préciser sur quel échantillon (taille, période)

#### Option B : Si les tests n'ont pas été finalisés
Ajouter une sous-section "Limites méthodologiques" dans la conclusion du chapitre 4 :

```latex
\subsubsection{Limites méthodologiques}

La validation empirique complète des modèles prédictifs sur données réelles n'a pu être finalisée dans le cadre de ce mémoire, pour les raisons suivantes :

\begin{itemize}
    \item \textbf{Contraintes d'accès aux données} : [préciser : confidentialité, approbations internes, etc.]
    \item \textbf{Période de mesure limitée} : [si applicable]
    \item \textbf{Volumétrie insuffisante} : [si applicable]
\end{itemize}

Les métriques de performance ($R^2$, MAE, RMSE) devront être calculées lors du déploiement opérationnel du modèle sur un échantillon test représentatif d'au moins [XX] deals traités.
```

**Action recommandée** : Privilégier l'option A si des données même partielles sont disponibles.

---

## 2. HARMONISATION DES NOTATIONS MATHÉMATIQUES

### Remarque
> Clarifier la séparation stricte entre les unités de temps (minutes) et les unités monétaires (euros) dans l'ensemble des formules du TDABC et du modèle Aftercare pour éviter toute ambiguïté.

### Fichiers concernés
- `sections/state-of-art.tex` (§2.1 ABC et TDABC)
- `sections/mesure.tex` (toutes les formules)
- `sections/modelisation.tex` (§4.1 reconstruction du coût)

### Modifications à effectuer

#### A. Créer une notation systématique dès le début

Dans **sections/state-of-art.tex**, après l'introduction du TDABC (§2.1), ajouter un encadré de notation :

```latex
\begin{tcolorbox}[colback=blue!5!white,colframe=blue!75!black,title=Convention de notation]
Pour éviter toute ambiguïté entre grandeurs temporelles et monétaires, nous adoptons la convention suivante dans l'ensemble du mémoire~:

\begin{itemize}
    \item \textbf{Grandeurs temporelles} (en minutes) : $t$, $\bar{t}$, $T$
    \item \textbf{Grandeurs monétaires} (en euros) : $C$, $w$
    \item \textbf{Conversion} : passage de minutes à heures via division par 60
\end{itemize}

Exemple : $C = \frac{T}{60} \times w$ où $T$ est en minutes, $w$ en €/h, et $C$ en €.
\end{tcolorbox}
```

#### B. Vérifier et corriger toutes les formules

**Dans sections/mesure.tex**, ligne 9-12 :
```latex
% AVANT
\bar{t} \approx 20\ \text{minutes}

% APRÈS (clarifier)
\bar{t} \approx 20\ \text{min}
```

**Dans sections/modelisation.tex**, ligne 10-18 :
```latex
% VÉRIFIER que l'unité est bien explicitée
C_{deal} = \sum_{i=1}^{N} \frac{T_{s,i}}{60}\,w_s
```

Ajouter un commentaire explicite :
```latex
\noindent où :
\begin{itemize}[noitemsep]
    \item $N$ : nombre d'événements (sans unité)
    \item $\bar{t} = 20$ : temps unitaire en \textbf{minutes}
    \item $T_{\text{AC}}$ : temps d'Aftercare en \textbf{minutes}
    \item $w_s = 60$ : coût horaire chargé en \textbf{€/h}
    \item $C_{deal}$ : coût total en \textbf{euros}
\end{itemize}
```

#### C. Vérifier systématiquement chaque formule

**Liste des formules à vérifier** (rechercher dans tous les fichiers) :
- [ ] Toute formule avec $t$, $T$, $\bar{t}$ : ajouter "(min)" ou "(minutes)"
- [ ] Toute formule avec $C$, $w$ : ajouter "(€)" ou "(€/h)"
- [ ] Toute conversion minute→heure : expliciter la division par 60
- [ ] Tableaux de résultats : ajouter les unités dans les en-têtes de colonnes

**Commande pour repérer les formules** :
```bash
grep -n "\\\\text{min}" sections/*.tex
grep -n "\\\\times" sections/*.tex
grep -n "\$C_" sections/*.tex
```

---

## 3. HOMOGÉNÉISATION DE LA CHARTE GRAPHIQUE

### Remarque
> Unifier le style visuel, les typographies et les palettes de couleurs de l'ensemble des figures et schémas conceptuels pour offrir un rendu visuel 100% professionnel.

### Fichiers concernés
- Toutes les figures TikZ dans `sections/contexte.tex`
- Toutes les figures TikZ dans `sections/state-of-art.tex`
- Toutes les figures TikZ dans `sections/mesure.tex`
- Toutes les figures TikZ dans `sections/modelisation.tex`

### Modifications à effectuer

#### A. Définir une charte graphique unifiée dans le préambule

Ajouter dans **packages.tex** (ou créer un fichier `tikz-styles.tex`) :

```latex
% ===== CHARTE GRAPHIQUE UNIFIÉE =====
\usepackage{xcolor}

% Palette de couleurs (adapter selon vos préférences)
\definecolor{primaryblue}{RGB}{31, 119, 180}
\definecolor{secondaryorange}{RGB}{255, 127, 14}
\definecolor{accentgreen}{RGB}{44, 160, 44}
\definecolor{lightgray}{RGB}{240, 240, 240}
\definecolor{darkgray}{RGB}{50, 50, 50}

% Styles TikZ réutilisables
\tikzset{
  % Boîtes de processus
  process/.style={
    rectangle, rounded corners=3pt, 
    draw=primaryblue, fill=primaryblue!10,
    line width=1pt, minimum width=25mm, minimum height=10mm,
    align=center, font=\small\bfseries
  },
  % Boîtes de données
  databox/.style={
    rectangle, rounded corners=2pt,
    draw=secondaryorange!70, fill=secondaryorange!5,
    line width=0.8pt, align=center, font=\footnotesize
  },
  % Notes explicatives
  note/.style={
    rectangle, rounded corners=2pt,
    draw=darkgray!30, fill=lightgray,
    text width=22mm, align=center, font=\tiny
  },
  % Flèches
  arrow/.style={->, >=Stealth, line width=1pt, color=darkgray},
  % Titres de sections dans diagrammes
  sectiontitle/.style={font=\small\bfseries\color{primaryblue}}
}
```

#### B. Inventaire des figures à harmoniser

**sections/contexte.tex** :
- [ ] Figure~\ref{fig:cyclevie} (ligne 22) : cycle de vie du crédit syndiqué
  - Remplacer `fill=blue!10` par `fill=primaryblue!10`
  - Remplacer `draw` par `draw=primaryblue`
  - Unifier la taille des nœuds : utiliser le style `process`

- [ ] Figure~\ref{fig:organigramme-loan-ops} : organigramme
  - Appliquer les mêmes couleurs
  - Vérifier que `font=\scriptsize\bfseries` est cohérent partout

**sections/state-of-art.tex** :
- [ ] Toutes les figures de schémas conceptuels
  - Remplacer les couleurs ad-hoc par la palette définie

**sections/mesure.tex** :
- [ ] Diagrammes de séparation EP/Aftercare
  - Unifier les couleurs

**sections/modelisation.tex** (ligne 22+) :
- [ ] Figure avec les modèles prédictifs
  - Style `panel/.style={rectangle, rounded corners=7pt, draw=#1!55, fill=#1!5...}`
  - Remplacer par les couleurs de la charte

#### C. Typographies à unifier

**Règles à appliquer partout** :
1. **Titres dans les figures** : `\small\bfseries`
2. **Labels dans les nœuds** : `\small` ou `\footnotesize` selon la taille
3. **Notes explicatives** : `\tiny`
4. **Épaisseur des traits** : `line width=1pt` pour les éléments principaux, `0.8pt` pour les secondaires
5. **Coins arrondis** : `rounded corners=3pt` pour les processus, `2pt` pour les notes

#### D. Plan d'action

1. **Étape 1** : Créer le fichier de styles communs
2. **Étape 2** : Parcourir chaque figure une par une
3. **Étape 3** : Remplacer les styles inline par les styles définis
4. **Étape 4** : Recompiler et vérifier visuellement la cohérence

**Commande pour lister toutes les figures** :
```bash
grep -n "\\begin{tikzpicture}" sections/*.tex
```

---

## 4. PEAUFINAGE DE LA TYPOGRAPHIE ET CORRECTION DES COQUILLES

### Remarque
> Effectuer une relecture typographique ciblée pour corriger les symboles isolés ou mal formatés ainsi que les espaces insécables manquants.

### Problèmes typographiques courants à rechercher

#### A. Espaces insécables manquants

**Règles françaises** :
- Avant `:`, `;`, `!`, `?` → espace insécable `~`
- Après `§` → espace insécable
- Entre nombre et unité → espace insécable
- Avant guillemets fermants `»` et après guillemets ouvrants `«`

**Recherches à effectuer dans tous les fichiers** :

```bash
# Rechercher les deux-points sans espace insécable
grep -n " :" sections/*.tex | grep -v "~:"

# Rechercher les points-virgules sans espace insécable
grep -n " ;" sections/*.tex | grep -v "~;"

# Rechercher les points d'exclamation/interrogation sans espace insécable
grep -n " ?" sections/*.tex | grep -v "~?"
grep -n " !" sections/*.tex | grep -v "~!"
```

**Correction type** :
```latex
% AVANT
Le coût est élevé : 60 euros.

% APRÈS
Le coût est élevé~: 60 euros.
```

**Note** : Certains fichiers utilisent déjà `\shorthandoff{;:!?}` pour désactiver babel, ce qui peut interférer. Vérifier la cohérence.

#### B. Espaces entre nombres et unités

```bash
# Rechercher les unités sans espace insécable
grep -nE "[0-9] (min|minutes|heures|euros|€|%)" sections/*.tex | grep -v "~"
```

**Correction type** :
```latex
% AVANT
20 minutes
60 euros

% APRÈS
20~minutes
60~euros
```

#### C. Symboles mathématiques isolés

**À rechercher** :
- Symboles `§` suivis d'un espace normal au lieu de `~`
- Références `§\ref{...}` : vérifier l'espace avant

```bash
grep -n "§ " sections/*.tex
```

**Correction** :
```latex
% AVANT
(§ 2.1)
comme expliqué au § 2.1

% APRÈS
(§~2.1)
comme expliqué au §~2.1 ou (§\ref{sec:abc})
```

#### D. Guillemets français

Vérifier que les guillemets utilisent bien la forme française :
```latex
% BON
«~texte~»

% À ÉVITER
"texte"
« texte »  % (sans espaces insécables)
```

#### E. Tirets

Trois types de tirets en LaTeX :
- Trait d'union : `-` (ex: "crédits syndiqués")
- Tiret demi-cadratin : `--` (ex: plages de pages "2--5")
- Tiret cadratin : `---` (ex: incise "le coût --- invisible jusqu'ici --- devient mesurable")

**Vérifier la cohérence** dans tout le document.

#### F. Coquilles et symboles mal formatés

**Liste de vérifications** :

- [ ] `\textit` vs `\emph` : privilégier `\emph` pour l'emphase sémantique
- [ ] Points finaux dans les légendes de figures/tableaux : être cohérent (avec ou sans)
- [ ] Majuscules après `:` : normalement minuscule sauf phrase complète
- [ ] `e.g.` vs `par exemple` : choisir français uniquement
- [ ] Espaces multiples : `  ` → ` `
- [ ] Retours à la ligne superflus : `\\ ` en fin de paragraphe

**Commandes de vérification** :
```bash
# Espaces multiples
grep -n "  " sections/*.tex

# Backslash-backslash en fin de paragraphe (souvent inutile)
grep -n "\\\\\\\\ *$" sections/*.tex
```

#### G. Cohérence des références bibliographiques

Vérifier dans **references.bib** et les citations :
- [ ] Format homogène des entrées BibTeX
- [ ] Pas de champs vides
- [ ] Accents et caractères spéciaux bien échappés
- [ ] `\cite` vs `~\cite` : espace insécable avant

**Exemple** :
```latex
% AVANT
selon Kaplan et Anderson (2007), le TDABC...

% APRÈS
selon Kaplan et Anderson~\cite{kaplan2007}, le TDABC...
```

---

## CHECKLIST COMPLÈTE DES MODIFICATIONS

### 1. Enrichissement empirique
- [ ] Ajouter tableau de métriques (R², MAE, RMSE) OU
- [ ] Ajouter section "Limites méthodologiques"

### 2. Harmonisation des notations mathématiques
- [ ] Créer encadré de convention de notation
- [ ] Vérifier toutes les formules (unités explicites)
- [ ] Ajouter unités dans les tableaux de résultats
- [ ] Vérifier cohérence temps (min) vs argent (€)

### 3. Homogénéisation charte graphique
- [ ] Définir palette de couleurs dans le préambule
- [ ] Créer styles TikZ réutilisables
- [ ] Modifier figure par figure (contexte.tex)
- [ ] Modifier figure par figure (state-of-art.tex)
- [ ] Modifier figure par figure (mesure.tex)
- [ ] Modifier figure par figure (modelisation.tex)
- [ ] Vérifier typographies dans les diagrammes
- [ ] Recompiler et vérifier visuellement

### 4. Peaufinage typographique
- [ ] Espaces insécables avant `:` `;` `!` `?`
- [ ] Espaces insécables après `§`
- [ ] Espaces insécables entre nombres et unités
- [ ] Guillemets français `«~...~»`
- [ ] Cohérence des tirets (-, --, ---)
- [ ] Espaces multiples
- [ ] Références bibliographiques
- [ ] Points finaux dans légendes

---

## ORDRE RECOMMANDÉ D'EXÉCUTION

1. **Jour 1** : Notations mathématiques (impact structurel, facile à vérifier)
2. **Jour 2** : Enrichissement empirique (requiert décision A ou B)
3. **Jour 3-4** : Charte graphique (long mais mécanique)
4. **Jour 5** : Typographie et relecture finale

---

## COMMANDES UTILES

### Recompiler le PDF
```bash
cd /Users/davidroufe/Pro/Dauphine/MÉMOIRE/thesis-template
latexmk -pdf main.tex
```

### Rechercher dans tous les fichiers
```bash
grep -r "pattern" sections/
```

### Compter les occurrences
```bash
grep -o "~:" sections/*.tex | wc -l
```

---

*Fin du document de modifications*
