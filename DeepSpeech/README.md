# 1. Description du modèle
[DeepSpeech](https://arxiv.org/abs/1412.5567) est un modèle de reconnaissance vocale open source développé par Mozilla. DeepSpeech est très flexible, s'adapte bien sur les données à l'entraînement grâce à sa capacité à identifier les bruits de fond et au modèle de langage inclut au moment de l'entraînement.

# 2. Entraîner son propre modèle
Pour entraîner le modèle, il faut avoir les pré-requis suivants:
- Python 3.6.
- Mac or Linux environment.
- CUDA 10.0 / CuDNN v7.6 par Dockerfile.

Il faut ensuite suivre les étapes suivantes:

## 2.1. Préparation de l'environnement
```shell script
# Importer le code du repository
git clone --branch v0.9.3 https://github.com/mozilla/DeepSpeech

# Créer un environnement virtuel
$ python3 -m venv $HOME/tmp/deepspeech-train-venv/
$ source $HOME/tmp/deepspeech-train-venv/bin/activate

# Installer le code pour l'entraînement et toutes ses dépendances
cd DeepSpeech
pip3 install --upgrade pip==20.2.2 wheel==0.34.2 setuptools==49.6.0
pip3 install --upgrade -e .
sudo apt-get install python3-dev

# Il est recommandé d'installer Tensorflow sur GPU, lorsqu'on dispose d'une machine NVIDIA avec au moins 8G de RAM
pip3 uninstall tensorflow
pip3 install 'tensorflow-gpu==1.15.4'
  
# Pour ceux qui veulent entraîner l'environnement sous Docker
make Dockerfile.train
make Dockerfile.train DEEPSPEECH_REPO=git://your/fork DEEPSPEECH_SHA=origin/your-branch

```
  
## 2.2. Charger la base de données
On suppose ici qu'on utilise la base de données de Mozilla Common Voice.
  
```shell script
bin/import_cv2.py --filter_alphabet path/to/some/alphabet.txt /path/to/extracted/language/archive
python3 DeepSpeech.py --train_files ../data/CV/en/clips/train.csv --dev_files ../data/CV/ar/clips/dev.csv --test_files ../data/CV/ar/clips/test.csv
```

## 2.3. Entraîner le modèle
L'entraînement du modèle est tout simple:
```shell script
python3 DeepSpeech.py --helpfull
./bin/run-ldc93s1.sh
```
Pour plus de personnalisation à l'entraînement du modèle, on vous recommande de suivre les étapes décrites [ici](https://deepspeech.readthedocs.io/en/r0.9/TRAINING.html).
