# Corrections suite aux remarques de la tutrice
*Date : 5 septembre 2026*

Ce document recense **uniquement** les modifications à effectuer suite aux **quatre remarques de la tutrice pédagogique**.

---

## REMARQUE 1 : ENRICHISSEMENT EMPIRIQUE DU VOLET PRÉDICTIF

### Remarque exacte
> Enrichissement empirique du volet prédictif : intégrer un tableau récapitulatif des métriques de performance ($R^2$, MAE, RMSE) sur données réelles pour valider les modèles XGBoost et Random Forest du Chapitre 4 (ou expliciter les contraintes d'accès aux données en tant que limite si ce test n'a pu être finalisé).

### Localisation
- **Fichier** : `sections/modelisation.tex`
- **Section** : Chapitre 4, après la présentation des modèles prédictifs

### Actions à réaliser

#### Option A : Si vous avez les données de performance
Ajouter un tableau dans le chapitre 4 :

```latex
\begin{table}[htbp]
\centering
\caption{Métriques de performance des modèles prédictifs sur données réelles}
\label{tab:metriques-performance}
\begin{tabular}{lccc}
\toprule
\textbf{Modèle} & \textbf{$R^2$} & \textbf{MAE (min)} & \textbf{RMSE (min)} \\
\midrule
Random Forest   & 0.XX & XX.X & XX.X \\
XGBoost        & 0.XX & XX.X & XX.X \\
\bottomrule
\end{tabular}
\small
\vspace{2mm}
\\
\textit{Note : Évaluation sur un échantillon de XX deals traités entre [dates].}
\end{table}
```

Accompagner d'un paragraphe d'analyse :
- Comparer les performances des deux modèles
- Interpréter le $R^2$ (part de variance expliquée)
- Commenter la précision (MAE, RMSE en minutes)
- Préciser la taille et la période de l'échantillon de test

#### Option B : Si vous n'avez pas finalisé les tests
Ajouter une sous-section dans le chapitre 4 ou dans la conclusion :

```latex
\subsubsection{Limite : validation empirique à finaliser}

La validation complète des modèles prédictifs sur données réelles n'a pu être achevée dans le cadre temporel du mémoire, en raison des contraintes suivantes :

\begin{itemize}
    \item \textbf{Contraintes d'accès aux données} : [détailler : confidentialité, validation interne, etc.]
    \item \textbf{Période de mesure limitée} : [si applicable]
    \item \textbf{Volumétrie de test insuffisante} : [si applicable]
\end{itemize}

Les métriques de performance standards ($R^2$, MAE, RMSE) devront être calculées lors du déploiement opérationnel sur un échantillon test représentatif d'au moins [XX] deals.
```

---

## REMARQUE 2 : HARMONISATION DES NOTATIONS MATHÉMATIQUES

### Remarque exacte
> Harmonisation des notations mathématiques : clarifier la séparation stricte entre les unités de temps (minutes) et les unités monétaires (euros) dans l'ensemble des formules du TDABC et du modèle Aftercare pour éviter toute ambiguïté.

### Fichiers concernés
- `sections/state-of-art.tex` (TDABC)
- `sections/mesure.tex` (toutes les formules de temps)
- `sections/modelisation.tex` (formules de coût)

### Actions à réaliser

#### A. Créer un encadré de notation dès l'état de l'art

Dans **sections/state-of-art.tex**, dans la section §2.1 sur le TDABC, ajouter :

```latex
\begin{tcolorbox}[colback=blue!5!white,colframe=blue!75!black,title=Convention de notation]
Pour éviter toute confusion entre grandeurs temporelles et monétaires, nous adoptons les conventions suivantes dans l'ensemble du mémoire~:

\begin{itemize}
    \item \textbf{Variables temporelles} (exprimées en minutes) : $t$, $\bar{t}$, $T$, $T_{\text{AC}}$
    \item \textbf{Variables monétaires} (exprimées en euros) : $C$, $w$
    \item \textbf{Passage minutes → heures} : division explicite par 60
\end{itemize}

\textbf{Exemple} : $C = \frac{T}{60} \times w$ où $T$ [min], $w$ [€/h], donc $C$ [€].
\end{tcolorbox}
```

*Note : Si `tcolorbox` n'est pas chargé, ajouter `\usepackage{tcolorbox}` dans packages.tex*

#### B. Expliciter les unités dans toutes les formules

**Dans sections/mesure.tex, équation (1) ligne 9-12** :
```latex
% Vérifier que c'est bien écrit :
\bar{t} \approx 20\ \text{min}
```

**Dans sections/modelisation.tex, équation du coût ligne 12-18** :

Ajouter un bloc explicatif après la formule :

```latex
\noindent où~:
\begin{itemize}[noitemsep]
    \item $N$ : nombre d'événements (sans dimension)
    \item $\bar{t} = 20$ : temps unitaire d'Event Processing en \textbf{minutes}
    \item $T_{\text{AC}}$ : temps total d'Aftercare en \textbf{minutes}
    \item $w_s = 60$ : coût horaire chargé en \textbf{€/h}
    \item $C_{\text{deal}}$ : coût opérationnel total en \textbf{euros}
\end{itemize}
```

#### C. Vérifier systématiquement toutes les formules

**Pour chaque équation du document** :
- [ ] Vérifier que les variables temporelles ont leur unité (min) précisée
- [ ] Vérifier que les variables monétaires ont leur unité (€ ou €/h) précisée
- [ ] Vérifier que chaque conversion minute→heure montre explicitement `/60`
- [ ] Dans les tableaux de résultats : ajouter les unités dans les en-têtes

**Méthode** : parcourir sections/mesure.tex et sections/modelisation.tex équation par équation.

---

## REMARQUE 3 : HOMOGÉNÉISATION DE LA CHARTE GRAPHIQUE

### Remarque exacte
> Homogénéisation de la charte graphique : unifier le style visuel, les typographies et les palettes de couleurs de l'ensemble des figures et schémas conceptuels pour offrir un rendu visuel 100% professionnel.

### Fichiers concernés
- Toutes les figures TikZ dans `sections/contexte.tex`
- Toutes les figures TikZ dans `sections/state-of-art.tex`
- Toutes les figures TikZ dans `sections/mesure.tex`
- Toutes les figures TikZ dans `sections/modelisation.tex`

### Actions à réaliser

#### Étape 1 : Définir une charte graphique unique

Créer un fichier **tikz-styles.tex** dans le dossier racine :

```latex
% ===== CHARTE GRAPHIQUE UNIFIÉE POUR TOUTES LES FIGURES =====

\usepackage{xcolor}

% Palette de couleurs du mémoire
\definecolor{primaryblue}{RGB}{31, 119, 180}      % Bleu principal
\definecolor{secondaryorange}{RGB}{255, 127, 14}  % Orange secondaire
\definecolor{lightgray}{RGB}{245, 245, 245}       % Gris clair fonds
\definecolor{darkgray}{RGB}{60, 60, 60}           % Gris foncé textes

% Styles TikZ réutilisables
\tikzset{
  % Style pour les boîtes de processus/étapes
  process/.style={
    rectangle, rounded corners=3pt, 
    draw=primaryblue, fill=primaryblue!10,
    line width=1pt, 
    minimum width=25mm, minimum height=10mm,
    align=center, 
    font=\small\bfseries
  },
  % Style pour les notes explicatives
  note/.style={
    rectangle, rounded corners=2pt,
    draw=darkgray!30, fill=lightgray,
    text width=22mm, 
    align=center, 
    font=\tiny
  },
  % Style pour les flèches
  arrow/.style={
    ->, >=Stealth, 
    line width=1pt, 
    color=darkgray
  }
}
```

Puis ajouter dans **main.tex** après `\input{packages}` :

```latex
\input{tikz-styles}
```

#### Étape 2 : Modifier toutes les figures

**Pour chaque figure TikZ du document** :

1. Remplacer les couleurs ad-hoc (`fill=blue!10`, `draw=red`, etc.) par les couleurs de la charte (`primaryblue`, `secondaryorange`, etc.)
2. Remplacer les styles inline par les styles définis (`process`, `note`, `arrow`)
3. Unifier les typographies :
   - Titres/labels principaux : `\small\bfseries`
   - Texte dans les boîtes : `\small` ou `\footnotesize`
   - Notes : `\tiny`
4. Unifier les paramètres géométriques :
   - Épaisseur des traits : `line width=1pt`
   - Coins arrondis : `rounded corners=3pt` pour processus, `2pt` pour notes

**Figures à modifier dans sections/contexte.tex** :
- [ ] Figure~\ref{fig:cyclevie} (ligne 22) : cycle de vie du crédit
- [ ] Figure organigramme Loan Ops (si présente)

**Figures à modifier dans sections/state-of-art.tex** :
- [ ] Tous les schémas conceptuels ABC/TDABC

**Figures à modifier dans sections/mesure.tex** :
- [ ] Diagrammes EP/Aftercare

**Figures à modifier dans sections/modelisation.tex** :
- [ ] Schémas des modèles prédictifs (ligne 22+)

#### Étape 3 : Vérification

Recompiler le PDF et vérifier visuellement que :
- [ ] Toutes les figures utilisent la même palette de couleurs
- [ ] Les typographies sont homogènes
- [ ] L'épaisseur des traits est cohérente
- [ ] Le rendu est professionnel

---

## REMARQUE 4 : PEAUFINAGE DE LA TYPOGRAPHIE ET CORRECTION DES COQUILLES

### Remarque exacte
> Peaufinage de la typographie et correction des coquilles : effectuer une relecture typographique ciblée pour corriger les symboles isolés ou mal formatés ainsi que les espaces insécables manquants.

### Fichiers concernés
Tous les fichiers .tex du dossier `sections/`

### Actions à réaliser

#### A. Espaces insécables en français

**Règles françaises** :
- Avant `:` → espace insécable `~:`
- Avant `;` → espace insécable `~;`
- Avant `!` → espace insécable `~!`
- Avant `?` → espace insécable `~?`
- Après `§` → espace insécable `§~`
- Entre nombre et unité → espace insécable `20~min`
- Guillemets : `«~texte~»`

**Méthode de recherche** :
```bash
# Trouver les deux-points sans espace insécable
grep -n " :" sections/*.tex | grep -v "~:"

# Trouver les points-virgules sans espace insécable  
grep -n " ;" sections/*.tex | grep -v "~;"

# Trouver les § sans espace insécable
grep -n "§ " sections/*.tex
```

**Correction type** :
```latex
% AVANT
Le coût est élevé : 60 euros.

% APRÈS
Le coût est élevé~: 60 euros.
```

#### B. Espaces entre nombres et unités

```bash
# Rechercher nombres suivis d'unités sans espace insécable
grep -nE "[0-9] (min|minutes|heures|euros|€|%)" sections/*.tex
```

**Correction** :
```latex
% AVANT
20 minutes, 60 euros, 5 %

% APRÈS
20~minutes, 60~euros, 5~\%
```

#### C. Symboles isolés ou mal formatés

- [ ] Vérifier tous les `§\ref{...}` : ils doivent avoir un espace insécable avant si dans le texte
- [ ] Vérifier les guillemets : utiliser `«~...~»` et non `"..."` ou `« ... »`
- [ ] Vérifier les tirets :
  - Trait d'union : `-`
  - Plage : `--` (ex: "2--5")
  - Incise : `---` (ex: "le coût --- invisible --- devient")

#### D. Références bibliographiques

Vérifier que les citations ont un espace insécable avant :

```latex
% AVANT
selon Kaplan (2007), ...

% APRÈS
selon Kaplan~\cite{kaplan2007}, ...
```

#### E. Relecture complète

**Checklist** :
- [ ] Parcourir sections/introduction.tex
- [ ] Parcourir sections/contexte.tex
- [ ] Parcourir sections/state-of-art.tex
- [ ] Parcourir sections/mesure.tex
- [ ] Parcourir sections/modelisation.tex
- [ ] Parcourir sections/conclusion.tex
- [ ] Vérifier references.bib (format homogène)

---

## RÉCAPITULATIF DES 4 REMARQUES

| # | Remarque | Fichiers principaux | Effort estimé |
|---|----------|-------------------|---------------|
| 1 | Enrichissement empirique | modelisation.tex | 2-4h |
| 2 | Notations mathématiques | state-of-art.tex, mesure.tex, modelisation.tex | 3-5h |
| 3 | Charte graphique | Tous les .tex avec TikZ | 6-8h |
| 4 | Typographie | Tous les sections/*.tex | 4-6h |

**Temps total estimé** : 15-23 heures de travail

---

## ORDRE RECOMMANDÉ

1. **Remarque 2** (notations) : impact structurel, relativement rapide
2. **Remarque 1** (tableau empirique) : décision A ou B à prendre
3. **Remarque 4** (typographie) : mécanique, peut se faire section par section
4. **Remarque 3** (charte graphique) : plus long, à faire en dernier

---

*Fin du document des remarques tutrice*
