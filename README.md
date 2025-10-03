# API de Reconnaissance de Chiffres MNIST

Ce projet est une application web simple qui reconnaît les chiffres manuscrits de la base de données MNIST. Il se compose d'un script Python pour entraîner un modèle de réseau de neurones et d'une API Flask pour servir les prédictions.

## Structure du Projet

- `train_model.py`: Script pour entraîner le modèle MNIST en utilisant TensorFlow/Keras et pour enregistrer les expériences avec MLflow.
- `app.py`: Une application Flask qui expose un point de terminaison `/predict` pour obtenir des prédictions de chiffres à partir du modèle entraîné.
- `requirements.txt`: Une liste des dépendances Python requises pour le projet.
- `Dockerfile`: Un fichier pour construire une image Docker pour l'application.
- `mnist_model.h5`: Le modèle entraîné (généré par `train_model.py`).

## Installation

1.  **Clonez le dépôt :**
    ```bash
    git clone <url-du-depot>
    cd <repertoire-du-depot>
    ```

2.  **Créez un environnement virtuel (recommandé) :**
    ```bash
    python3 -m venv venv
    source venv/bin/activate
    ```

3.  **Installez les dépendances :**
    ```bash
    pip install -r requirements.txt
    pip install mlflow
    ```
    *Note : `mlflow` est utilisé pour le suivi des expériences dans `train_model.py`.*

## Utilisation

### 1. Entraînez le Modèle

Pour entraîner le modèle, exécutez le script `train_model.py` :

```bash
python train_model.py
```

Cela entraînera un nouveau modèle sur l'ensemble de données MNIST, le sauvegardera sous le nom `mnist_model.h5`, et enregistrera les paramètres et les métriques d'entraînement à l'aide de MLflow.

### 2. Exécutez l'API Flask

Pour démarrer le serveur Flask, exécutez le script `app.py` :

```bash
python app.py
```

L'application sera disponible à l'adresse `http://localhost:5000`.

### 3. Obtenez des Prédictions

Vous pouvez envoyer une requête POST au point de terminaison `/predict` avec une charge utile JSON contenant les données de l'image. L'image doit être un tableau aplati de 784 éléments de valeurs de pixels (image 28x28).

Voici un exemple avec `curl` :

```bash
curl -X POST -H "Content-Type: application/json" -d '{"image": [<vos_784_valeurs_de_pixels>]}' http://localhost:5000/predict
```

Remplacez `<vos_784_valeurs_de_pixels>` par les données réelles de l'image.

## Docker

Vous pouvez également construire et exécuter l'application à l'aide de Docker.

1.  **Construisez l'image Docker :**
    ```bash
    docker build -t mnist-api .
    ```

2.  **Exécutez le conteneur Docker :**
    ```bash
    docker run -p 5000:5000 mnist-api
    ```

L'API sera accessible à l'adresse `http://localhost:5000`.
