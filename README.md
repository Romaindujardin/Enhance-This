# Enhance-This

## Super-Resolution d’Images par GAN  
## Étude Progressive de Trois Architectures SRGAN

---

## 1. Présentation du projet

Ce projet vise à implémenter et améliorer progressivement un modèle de super-résolution d’images basé sur les Generative Adversarial Networks (SRGAN).

L’objectif est de reconstruire une image haute résolution (HR) à partir d’une image basse résolution (LR), en maximisant à la fois :

- la fidélité pixel (mesures objectives comme le PSNR),
- la qualité perceptuelle (textures réalistes),
- la stabilité d’entraînement du GAN.

Trois versions successives ont été développées afin d’améliorer progressivement :

- la qualité du dataset,
- la structure du générateur,
- la stratégie d’entraînement,
- les fonctions de perte,
- la stabilité globale du modèle.

---

# 2. Version 1 – Implémentation de base

Fichier : `SR-GAN_version1.ipynb`

## Objectif

Mettre en place une première implémentation fonctionnelle d’un SRGAN simplifié.

## Caractéristiques principales

- Dataset simple et limité  
- Images de petite taille (patches 96×96)  
- Générateur avec architecture résiduelle standard  
- Discriminateur convolutionnel classique  
- Loss combinée :
  - Pixel loss (L1 ou MSE)  
  - Adversarial loss  
- Pas ou peu de pré-entraînement séparé du générateur  

## Limites observées

- Dataset trop restreint pour une généralisation robuste  
- Lissage excessif des textures  
- PSNR limité  
- Entraînement GAN parfois instable  
- Peu de métriques pour analyser finement la convergence  

## Intérêt académique

Cette version constitue une base expérimentale.  
Elle permet de comprendre la mécanique GAN appliquée à la super-résolution.

---

# 3. Version 2 – Amélioration du Dataset et de l’Entraînement

Fichier : `SR-GAN_version2.ipynb`

## Objectif

Améliorer la robustesse du modèle en travaillant principalement sur :

- la qualité du dataset,  
- la procédure d’entraînement,  
- la taille des images.  

## Améliorations majeures

### 1. Dataset plus riche

- Jeu de données plus diversifié  
- Meilleure distribution des textures  
- Génération contrôlée des paires LR/HR  

**Impact :**

- Meilleure généralisation  
- Réduction du sur-apprentissage  

---

### 2. Augmentation de la taille d’entrée

Passage au-delà de 96×96.

**Impact :**

- Contexte spatial plus large  
- Reconstruction de structures plus cohérentes  

---

### 3. Normalisation et activation

- Meilleure normalisation des données  
- Remplacement de certaines activations inadaptées (ex : Sigmoid en sortie si non pertinente)  
- Stabilisation numérique  

---

### 4. Stratégie d’entraînement plus propre

- Séparation claire entre phase warmup (pixel loss uniquement)  
- Phase GAN ensuite  
- Suivi du PSNR pendant l’entraînement  

## Résultats

- PSNR en progression stable  
- Discriminateur plus équilibré  
- Générateur plus stable  
- Moins d’artefacts visuels  

## Positionnement

Cette version marque une transition vers un pipeline sérieux et reproductible.

---

# 4. Version 3 – Pipeline Stabilisé et Plus Perceptuel

Fichier : `SR_GAN.ipynb`

## Objectif

Construire une version plus aboutie et académiquement cohérente du SRGAN.

## Améliorations clés

### 1. Pré-entraînement structuré (Warmup)

Le générateur est d’abord entraîné uniquement avec une pixel loss.

**But :**

- Obtenir une reconstruction stable  
- Fournir un bon point de départ au GAN  
- Éviter l’effondrement précoce  

---

### 2. Loss perceptuelle (Feature Loss)

Ajout d’une loss basée sur un réseau pré-entraîné (ex : VGG).

**Impact :**

- Meilleure reconstruction des textures  
- Meilleure cohérence perceptuelle  
- Images moins lissées  

---

### 3. Combinaison pondérée des pertes

Loss finale typique :

- Pixel loss  
- Content loss (features)  
- Adversarial loss pondérée  

Cela permet de contrôler le compromis :

- fidélité objective (PSNR),  
- qualité visuelle subjective.  

---

### 4. Suivi métrique structuré

Ajout de métriques telles que :

- PSNR  
- Loss générateur  
- Loss discriminateur  

Permet :

- d’analyser la stabilité,  
- d’identifier les plateaux,  
- d’observer l’équilibre G/D.  

## Résultats observés

- PSNR stabilisé autour d’un plateau cohérent  
- Discriminateur équilibré (pas de collapse)  
- Générateur stable sur plusieurs dizaines d’epochs  
- Résultats visuels plus réalistes  
- Absence d’artefacts majeurs  

## Niveau atteint

Cette version correspond à une implémentation solide d’un SRGAN académique :

- stable,  
- reproductible,  
- correctement structuré.

## Résultat
<img width="1570" height="500" alt="Unknown" src="https://github.com/user-attachments/assets/b64aa02c-a511-4112-a227-132a48f959cb" />


---

# 5. Comparaison Synthétique

| Critère | Version 1 | Version 2 | Version 3 |
|----------|------------|------------|------------|
| Dataset | Basique | Amélioré | Structuré et robuste |
| Taille images | 96×96 | Supérieure | Supérieure |
| Warmup | Non structuré | Partiel | Oui |
| Loss perceptuelle | Non | Partielle | Oui |
| Stabilité GAN | Moyenne | Bonne | Stable |
| Suivi métrique | Limité | Correct | Structuré |
| Robustesse globale | Faible | Moyenne | Élevée |

---

# 6. Contribution du projet

Ce projet montre une progression méthodologique claire :

1. Implémentation naïve  
2. Amélioration des données et de la stabilité  
3. Intégration de principes avancés de super-résolution perceptuelle  

Il démontre :

- la sensibilité des GAN à la qualité du dataset,  
- l’importance du pré-entraînement,  
- l’impact du choix des fonctions de perte,  
- le compromis entre PSNR et qualité perceptuelle.  

---

# 7. Perspectives d’amélioration

Pour aller plus loin :

- Implémenter un Relativistic GAN  
- Passer à une architecture ESRGAN (RRDB blocks)  
- Ajouter SSIM comme métrique  
- Tester différents coefficients de pondération  
- Évaluer sur benchmarks standards (DIV2K, Set5, Set14)  

---

# 8. Conclusion

Les trois versions illustrent une montée en complexité et en rigueur méthodologique.

La version 1 valide le concept.  
La version 2 améliore la robustesse expérimentale.  
La version 3 atteint un niveau académique cohérent et stable.

Le projet constitue une base solide pour une étude comparative, une extension vers ESRGAN ou une publication académique appliquée à la super-résolution d’images.
