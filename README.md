# Email Spam Ham - TP complié sur Google Colab 

Choix techniques
1. Vectorisation du texte

    Méthode : TF-IDF (Term Frequency-Inverse Document Frequency).
    Pourquoi TF-IDF ?
        TF-IDF pour représenter le texte sous forme numérique.
        Elle capture l'importance des mots dans un document tout en réduisant le poids des mots fréquents mais peu significatifs (e.g., "the", "and").
    Paramètres choisis :
        max_features=1000 : Limite le vocabulaire à 1 000 mots les plus fréquents, pour réduire la complexité et la consommation mémoire ( car j'ai eu un problème de ram sur Colab )
        stop_words='english' : Exclut les mots courants inutiles en anglais ('the', 'a')

    Binary_crossentropy : Car on cherche à résoudre un problème de classification binaire. Elle mesure la probabilité pédite et la vérité.

    L2 Regularization (kernel_regularizer=l2(0.01)) : Pour éviter le overfiting, elle ajoute une pénalité au cout total de la fonction de perte quand on a des grand poids  comme ça on évite notre modèle fait que mémoriser et pas apprendre

    Dropout (30%)

    Désactive aléatoirement 30% des neurones pendant l'entraînement.
    Encourage le modèle à généraliser au lieu de mémoriser.

2. Architecture du modèle

    Le modèle est composé de 3 couches :

    Couche d'entrée :

        La première couche est une couche Dense avec 128 neurones avec la fonction d'activatio relu car elle accélérer la convergence du gradient. Et Prend les données que TD-IDF à générer.
            
    Couche cachée :

        La deuxième couche est une autre couche Dense avec 64 neurones avec une relu.
    Couche de sortie :

        La dernière couche est une couche Dense avec 1 neurone et segmoid car c'est un problème binaire qu'on souhaite résoudre (Spam ou Ham)

3. Callbacks

    EarlyStopping
        Arrête automatiquement l'entraînement si la perte de validation cesse de s'améliorer (patience de 3 epochs).
        Évite l'entraînement inutile et le surapprentissage.

    ReduceLROnPlateau
        Réduit dynamiquement le learning rate lorsque la perte de validation stagne (patience de 3 epochs).
        Permet au modèle de continuer à apprendre plus finement.

    TensorBoard
        Permet de visualiser les métriques d'entraînement et de validation en temps réel.


4. Résulta:

    Classe 0 (Ham) :

    Précision : 96% - La plupart des emails Ham sont correctement identifiés.
    Rappel : 95% - Très peu d'emails Ham sont incorrectement classés comme Spam.
    F1-Score : 95% - Bon équilibre entre précision et rappel.

    Classe 1 (Spam) :

    Précision : 94% - La majorité des emails Spam sont correctement identifiés.
    Rappel : 95% - Peu d'emails Spam sont manqués.
    F1-Score : 95% - Solide performance globale.

    Performance globale :
        Exactitude (accuracy) : 95% sur 38 771 emails.
        