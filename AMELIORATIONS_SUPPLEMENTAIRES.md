# Améliorations supplémentaires suggérées
*Date : 5 septembre 2026*

Ce document recense mes **suggestions personnelles** d'amélioration, au-delà des remarques de la tutrice.

---

## 1. COHÉRENCE TERMINOLOGIQUE

### Observation
En parcourant le mémoire, j'ai remarqué que certains termes sont parfois utilisés de façon interchangeable.

### Suggestions

#### A. Uniformiser "Event Processing" vs "traitement d'événements"
- [ ] Décider : garder l'anglais partout OU traduire systématiquement en français
- [ ] Si anglais : mettre en italique à la première occurrence puis roman
- [ ] Si français : "traitement d'événements" avec majuscule comme terme technique

#### B. "Deal" vs "crédit" vs "contrat"
- [ ] Vérifier que "deal" est le terme retenu (semble être le cas)
- [ ] S'assurer qu'il est défini clairement dans le glossaire
- [ ] Vérifier qu'il n'y a pas d'alternance non intentionnelle

#### C. Acronymes
- [ ] Vérifier que tous les acronymes sont définis à leur première occurrence
- [ ] Vérifier la cohérence : ABC, TDABC, EP, LS, etc.
- [ ] S'assurer que le glossaire est complet

---

## 2. STRUCTURE DES PARAGRAPHES

### Observation
Quelques paragraphes sont très longs, ce qui peut nuire à la lisibilité.

### Suggestions

#### sections/introduction.tex
- Ligne 7 : le paragraphe sur GTS2025 et GB Indus fait ~15 lignes
  - [ ] Envisager de le scinder en deux : contexte stratégique / déclinaison opérationnelle

#### sections/state-of-art.tex
- Le paragraphe d'introduction (lignes 5-22) est dense
  - [ ] Possibilité de l'aérer avec un saut de ligne après "le coût, puis à la rentabilité."

---

## 3. FIGURES ET TABLEAUX

### Observation
Certaines figures pourraient bénéficier de légendes plus explicites.

### Suggestions

#### A. Légendes des figures
- [ ] Vérifier que chaque légende peut être comprise sans lire le texte
- [ ] Format recommandé : "Figure X. [Titre court]. [Phrase explicative optionnelle]"
- [ ] Exemple actuel à vérifier : Figure cyclevie (contexte.tex ligne 22)

#### B. Numérotation et références
- [ ] Vérifier que toutes les figures sont référencées dans le texte
- [ ] Vérifier que les références sont avant ou après la figure, jamais trop loin
- [ ] Format : toujours `figure~\ref{...}` (avec espace insécable)

#### C. Tableaux manquants potentiels
- [ ] Envisager un tableau récapitulatif "Comparaison ABC vs TDABC" dans state-of-art.tex
- [ ] Envisager un tableau "Avantages/Limites des méthodes prédictives" dans modelisation.tex

---

## 4. BIBLIOGRAPHIE

### Observation
La bibliographie semble fonctionnelle mais pourrait être enrichie.

### Suggestions

#### A. Vérifier la source "finance-club"
Dans contexte.tex ligne 19 :
```latex
% TODO : remplacer finance-club par une source solide
```
- [ ] Remplacer par une source académique (Loan Market Association, manuel de finance)

#### B. Homogénéité du fichier references.bib
- [ ] Vérifier que tous les champs sont remplis (auteur, année, titre)
- [ ] Vérifier les accents (é → {\'e} ou utiliser biblatex)
- [ ] Vérifier qu'il n'y a pas de champs vides

#### C. Citations dans le texte
- [ ] Privilégier `\cite` avec contexte plutôt que citations nues
- [ ] Exemple : "Selon \citeauthor{kaplan2007}, ..." plutôt que "Kaplan (2007) dit que..."

---

## 5. CODE ET FORMULES LATEX

### Observation
Quelques petites optimisations possibles du code LaTeX.

### Suggestions

#### A. Packages
Vérifier dans packages.tex :
- [ ] Certains packages sont-ils en double ?
- [ ] Certains packages sont-ils obsolètes ? (ex: `epsfig` → `graphicx`)
- [ ] L'ordre de chargement est-il optimal ? (hyperref en dernier généralement)

#### B. Commandes personnalisées
Envisager de créer des commandes pour les termes récurrents :
```latex
% Dans packages.tex ou un nouveau fichier commands.tex
\newcommand{\tdabc}{\textit{Time-Driven Activity-Based Costing}}
\newcommand{\ep}{\textit{Event Processing}}
\newcommand{\ac}{\textit{Aftercare}}
```

Avantage : facilite les changements de mise en forme globaux.

#### C. Environnements mathématiques
- [ ] Vérifier qu'on utilise `equation` (numérotée) vs `equation*` (non numérotée) de façon intentionnelle
- [ ] Toutes les équations importantes sont-elles numérotées et référencées ?

---

## 6. COHÉRENCE DES EXEMPLES NUMÉRIQUES

### Observation
Des valeurs numériques sont utilisées (20 min, 60 €/h, etc.).

### Suggestions

#### A. Vérifier la cohérence
- [ ] Le temps unitaire est-il toujours ~20 min partout ?
- [ ] Le coût horaire est-il toujours 60 €/h ?
- [ ] Si ces valeurs varient, est-ce explicité ?

#### B. Précision des arrondis
- [ ] Décider d'une règle : 1 chiffre après la virgule ? 2 ?
- [ ] Appliquer uniformément

---

## 7. TRANSITIONS ENTRE SECTIONS

### Observation
Les transitions entre chapitres pourraient être renforcées.

### Suggestions

#### A. Fin de chaque chapitre
Envisager d'ajouter un court paragraphe de transition :
- [ ] Fin de l'introduction → annonce du chapitre 2
- [ ] Fin de state-of-art → annonce du chapitre 3
- [ ] Fin de mesure → annonce du chapitre 4

Format type :
> "Le chapitre suivant exploite ces fondements théoriques pour construire..."

#### B. Début de chaque chapitre
Vérifier qu'il y a un paragraphe d'introduction qui :
- Rappelle brièvement où on en est
- Annonce ce que va faire le chapitre
- Explique le lien avec le précédent

---

## 8. GLOSSAIRE

### Observation
Le fichier glossaire.tex existe mais je n'ai pas pu le lire.

### Suggestions
- [ ] Vérifier que tous les termes techniques sont définis
- [ ] Ordre alphabétique
- [ ] Format homogène
- [ ] Termes à inclure obligatoirement :
  - Deal
  - Event Processing
  - Aftercare
  - TDABC
  - ABC
  - Loan Servicing
  - Front Office, Middle Office, Back Office
  - Nearshoring

---

## 9. ABSTRACT/PRÉAMBULE

### Observation
Il existe un fichier abstract.tex (préambule).

### Suggestions
- [ ] Vérifier qu'il résume bien les 4 chapitres
- [ ] Vérifier qu'il mentionne la contribution principale
- [ ] Vérifier qu'il ne dépasse pas 1 page
- [ ] Le relire en dernier (après toutes les modifications) pour cohérence

---

## 10. REMERCIEMENTS

### Observation
Fichier thanks.tex existe.

### Suggestions
- [ ] Vérifier que tous les acteurs importants sont mentionnés :
  - Tutrice pédagogique
  - Tuteur entreprise
  - Équipes BNP
  - Collègues/amis
- [ ] Vérifier l'orthographe des noms
- [ ] Ton approprié (ni trop formel, ni trop familier)

---

## 11. VALIDATION FINALE

### Suggestions de tests avant soumission

#### A. Tests de compilation
- [ ] Le PDF compile sans erreur
- [ ] Le PDF compile sans warning grave
- [ ] Toutes les références sont résolues (pas de "??")
- [ ] La table des matières est correcte
- [ ] La liste des figures est correcte
- [ ] La bibliographie s'affiche correctement

#### B. Vérifications visuelles
- [ ] Pas de débordement de texte dans les marges
- [ ] Pas de figures qui "flottent" trop loin de leur référence
- [ ] Numérotation des pages cohérente (romain puis arabe)
- [ ] En-têtes et pieds de page corrects

#### C. Cohérence globale
- [ ] Relire l'introduction et la conclusion : sont-elles cohérentes ?
- [ ] Le titre du mémoire reflète-t-il bien le contenu ?
- [ ] Les objectifs annoncés dans l'intro sont-ils remplis dans la conclusion ?

---

## 12. OUTILS RECOMMANDÉS

### Pour faciliter les corrections

#### A. Correction orthographique
```bash
# Si aspell est installé
aspell --lang=fr check sections/introduction.tex
```

#### B. Recherche de patterns
```bash
# Trouver toutes les équations
grep -n "\\begin{equation" sections/*.tex

# Trouver toutes les figures
grep -n "\\begin{figure" sections/*.tex

# Trouver tous les tableaux
grep -n "\\begin{table" sections/*.tex
```

#### C. Comptage de mots (approximatif)
```bash
# Compter les mots dans tous les .tex
detex sections/*.tex | wc -w
```

---

## PRIORITÉS

### Priorité HAUTE (à faire)
- Point 4.A : corriger la source "finance-club"
- Point 8 : vérifier le glossaire
- Point 11 : validation finale

### Priorité MOYENNE (recommandé)
- Point 1 : cohérence terminologique
- Point 3 : améliorer les légendes
- Point 7 : transitions entre sections

### Priorité BASSE (optionnel)
- Point 5 : optimisations LaTeX
- Point 2 : structure des paragraphes
- Point 12 : outils (si besoin)

---

*Fin des suggestions d'amélioration*
