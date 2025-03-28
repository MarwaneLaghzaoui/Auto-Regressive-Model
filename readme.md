
AUTOREGRESSIVE MODEL

Un modèle autoregressif est un type de modèle où chaque prédiction dépend des valeurs précédemment générées. Pour une image, un pixel ou un élément est prédit en fonction des éléments déjà prédits, créant ainsi une séquence qui se construit progressivement. Cela permet au modèle de générer des données complexes de manière cohérente.

Dans ce TP, on va utiliser un modèle autoregressif pour générer des images. Le modèle PixelCNN est utilisé, où chaque pixel d'une image est prédit en fonction des pixels précédemment générés. Pour ce faire, des convolutional layers sont appliquées afin de garantir que chaque pixel n'influence que les pixels précédents, et non ceux qui viennent après. Ce processus est combiné avec des blocs résiduels. L'entraînement du modèle consiste à ajuster les poids pour minimiser l'erreur entre les pixels prédits et les pixels réels, permettant ainsi de générer des images cohérentes une fois l'apprentissage terminé.