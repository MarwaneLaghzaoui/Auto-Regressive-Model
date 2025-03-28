# PixelCNN pour la génération d'images

Le data set que nous allons étudier est fashion MNIST, un dataset contenant des images 28x28 en noir et blanc représentant différents types d'habits, par exemple chaussures, pulls 
t-shirt pantalons etc. 

# Etude des parametres

Afin d'alleger l'entrainement, les images seront ramennées à 16x16.
Pixel_levels sert à garder seulement quatre niveaux de couleur (noir, gris clair, gris foncé, blanc) afin de simplifier le probleme de prédiction de la couleur.
Les 128 filtres sont les matrices de poids qui serviront à la detection des formes et patterns à apprendre.
Residual block va permettre de reduire la complexité du réseau de neuronnes 

# Preprocess

On applique simplement le nouveau format de l'image 16x16 et on réduit les valeurs de pixels à 0 1 2 ou 3, enfin on transforme les images en tenseurs

# Masked convolution

On va appliquer Une convolution avec comme étape supplémentaire le masque M. Les masque va permettre aux pixels de ne jamais connaitres les pixels suivant, creant ainsi le comportement autoregressif désiré. Le but du masked convolution layer va etre de rendre nul les poids des pixels suivants afin de les masquer. Pour cela on va creer un masque
de la taille de notre kernel et le remplir de 1. Ensuite les poids qui sont placé en bas et à droite du pixel du masque central sont mit à 0 et si le masque est de type A, le pixel central sera 0 sinon 1. Enfin on effectue le produit entre la matrice des poids et du masque et on obtient bien un kernel de poids qui ne connait pas ceux des pixels suivants.

# Residual block

Il s'agit d'un eéseau de convolutionnel qui va permettre de garantir la stabilité du model tout en préservant sa profondeur car augmenter la profondeur du réseau peut etre contreproductif si mal optimisé. 

# Pixel CNN

Il s'agit du réseau de neuronnes utilisant nos masques de convolution et les blocks résiduels. La premiere couche est de type A comme, de taille de kernel 7x7, le padding = 3 va permettre de garder la meme taille d'image puisque l'on ajoute 6 pixels à la largeur et hauteur de l'image. Une fois cette couche passée, nous appliquons le bloque résiduel 5 fois. Ensuite deux couches masquées de types B et enfin une couche de convolution classique, avec des couches relu pour introduire la non linéarité.

# Training

Optimizer : Adam avec un learning rate de 1e-4 qui permet de garantir un entrainement assez lent pour 150 epoques. 
Criterion : CrossEntropy. Il s'agit d'une fonction de perte qui permet d'évaluer le lien entre deux éléments. Plus la probabilité que le pixel appartient à la bonne classe est proche de 1, plus le produit yx * log(xc) sera proche de 0 donc la fonction de perte sera basse. A l'inverse, si la probabiltié prédite de x est proche de 0, plus log se rapproche de l'infini donc la fonction de perte sera élevée.

Boucle d'entrainement :

Pour chaque epoque et pour chaque image, nous allons envoyer l'image au model qui va essayer de predire la prbabilité le prochain pixel appartient à un chacun des quatres pixel level, par exemple [0.1,0.2,0.3,0.4] ensuite, la matrice est envoyée à la fonction de perte qui va comparer avec l'image réelle et évaluer la perte.
Ensuite on va calculer les gradients des poids avec loss.backward() et mettre à jours les poids avec optimizer.step()

Maintenant que le model est entrainé, on peux generer des images et les observer.
