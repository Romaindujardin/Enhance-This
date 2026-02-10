# Enhance-This
Super-résolution d’images par autoencodeur convolutionnel.

## Notebook Colab prêt à l'emploi
- `colab_cae_super_resolution.ipynb` : pipeline complète en Python pour entraîner un **CAE (Convolutional Autoencoder)** qui prend une image basse qualité en entrée et reconstruit une image de meilleure qualité.

Le notebook couvre :
1. Chargement des données (CIFAR-10).
2. Génération d’images basse qualité (downsample + upsample + bruit).
3. Définition et entraînement d’un CAE.
4. Visualisation des résultats (LQ vs sortie CAE vs HQ).
5. Sauvegarde du modèle entraîné.
