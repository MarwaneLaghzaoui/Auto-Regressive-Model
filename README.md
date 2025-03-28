# Ugo Merlier 2024/2025 Ing3 IA B

## Autoregressive Models (PixelCNN)

![Exemple de sortie](./assets/front.png)

## Introduction
<p align="justify">
Dans ce TP nous allons expliquer en détails le fonctionnement du modèle PixelCNN à travers un code donné en exemple. Tout d’abord, définissons rapidement comment fonctionne un modèle autorégressif. Dans cette famille on en compte 4, le RNN, le LSTM, le GRU et enfin le transformer. Chacun a sa propre spécificité mais prenons pour base le RNN (Recurent neural network) afin de bien comprendre le fonctionnement des autorégressifs modèles. Le RNN est très utiles notamment pour la prédiction de petites séries temporelles. Pour le reste de l’explication nous prendrons pour exemple la prédiction du prix des patates. Le modèle prend deux paramètres en entrés. Les inputs nécessaires à la prédiction à l’instant T, par exemple, la quantité de patate produite, les intempéries ect…. Mais également la valeur réel ou prédite précédente de notre variable de prédiction, ici, le prix de notre patate. On précise, réel ou prédite car généralement on commence par données des valeurs réels pour initialiser notre modèle et par la suite on lui donne les valeurs qu’il vient de prédire. On se retrouve donc avec une boucle où le modèle utilise le résultat de sa précédente prédiction pour prédire la suivante. On voit bien le cheminement sur le schéma ci-dessous.

</p>


