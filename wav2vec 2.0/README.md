# 1. Description du modèle
Nous proposons dans ce projet un fine-tuning du modèle XLSR-wav2vec2.0. XLSR-53, pour "Unsupervised Cross-Lingual Representation Learning For Speech Recognition" est une version multilingue du modèle [wav2vec 2.0: A Framework for Self-Supervised Learning of Speech Representations (Baevski et Al., 2020)](https://arxiv.org/abs/2006.11477). Il a été entraîné sur trois bases de données reparties sur 53 langues pour un total de 56.000 heures d'audios.

Modèle | Architecture | Nombre d'heures | Langues | Datasets | Lien
|---|---|---|---|---|---
XLSR-53 | Large | 56k | 53 | MLS, CommonVoice, BABEL | [Télécharger](https://dl.fbaipublicfiles.com/fairseq/wav2vec/xlsr_53_56k.pt)

XLSR-53 détecte les paramètres sur des données non annotées comme il est décrit sur [Unsupervised Cross-lingual Representation Learning for Speech Recognition (Conneau et Al. 2020)](https://arxiv.org/abs/2006.13979). Pour effectuer le fine-tuning sur le Darija et l'Arabe on utilise une Classification Temporelle Connexionniste (CTC) sur des données annotées. CTC est un algorithme utilisé sur des réseaux de neurones pour des problèmes de séquence à séquence, dans notre cas, pour la reconnaissance automatique de la parole. Il permet d'identifier des labels sur les échantillons d'audios d'entraînement.

<table>
  <tr>
    <th><b>Version</b></th>
    <th><b>Source</b></th>
    <th><b>Taille</b></th>
    <th><b>Langue</b></th>
    <th><b>Speech Augmentation</b></th>
    <th><b>WER</b></th>
    <th><b>Durée</b></th>
    <th><b>Epochs</b></th>
    <th><b>Demo</b></th>

  </tr>

  <tr>
    <td>Bêta</td>
    <td>Mozilla Common Voice</td>
    <td>1500</td>
    <td>Arabe</td>
    <td>Non</td>
    <td>0.7</td>
    <td>-</td>
    <td>30</td>
    <td><a href="https://dvoice.ma/demo"><img style="height:20px;" src="https://dvoice.ma/logos/logo-transparent.png"></a></td>
  </tr>

  <tr>
    <td>Bêta 2</td>
    <td>Facebook / Youtube</td>
    <td>2400</td>
    <td>Darija</td>
    <td>Non</td>
    <td>0.9</td>
    <td>5h</td>
    <td>30</td>
    <td>--------</td>
  </tr>

  <tr>
    <td>Version 1.0</td>
    <td>Facebook / Youtube / Dvoice</td>
    <td>13000</td>
    <td>Darija</td>
    <td>Oui</td>
    <td>0.3</td>
    <td>5h</td>
    <td>10</td>
    <td><a href="https://dvoice.ma/demo"><img style="height:20px;" src="https://dvoice.ma/logos/logo-transparent.png"></a></td>
  </tr>

  
  
<table>

- WER : Word Error Rate

# 2. Entraînement du modèle "from scratch"
Pour entraîner un modèle XLSR-53 "from scratch", nous recommandons de suivre les étapes décrit [ici](https://github.com/pytorch/fairseq/tree/master/examples/wav2vec). On y retrouve l'ensemble des modèles du projet wav2vec y compris sa version multilingue XLSR-53.
  
- PyTorch version >= 1.5.0
- Python version >= 3.6
- Pour entraîner de nouveaux modèles on a besoin d'avoir un GPU NVIDIA et [NCCL](https://github.com/NVIDIA/nccl).
- Installation pour un dévéloppement en local:

``` bash
git clone https://github.com/pytorch/fairseq
cd fairseq
pip install --editable ./

# on MacOS:
# CFLAGS="-stdlib=libc++" pip install --editable ./

# to install the latest stable release (0.10.x)
# pip install fairseq
```
Pour un entraînement rapide, installer la librairie [apex](https://github.com/NVIDIA/apex) de NVIDIA:

``` bash
git clone https://github.com/NVIDIA/apex
cd apex
pip install -v --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" \
  --global-option="--deprecated_fused_adam" --global-option="--xentropy" \
  --global-option="--fast_multihead_attn" ./
```
Lorsque la dataset est trop volumineuse, installer [PyArrow](https://arrow.apache.org/docs/python/install.html#using-pip) : `pip install pyarrow`.  

#### a. Entrainement depuis une ligne de commandes
Le modèle prend en entrée des fichiers. Il est recommandé de fragmenter les audios en morceaux de 10 à 30 secondes.
- Préparation

Installer la librairie `soundfile`:
```shell script
pip install soundfile
```

Ensuite:

```shell script
$ python wav2vec/wav2vec_manifest.py /path/to/waves --dest /manifest/path --ext $ext --valid-percent $valid
```
$ext : peut être n'importe quel format audio (mp3, flav, wav,...) tant que sounfile peut lire.
  
$valid : prendre une petite portion (10% par exemple) des données d'entraînement pour la validation

#### b. Entraînement du modèle wav2vec2.0 de base
Les audios entrée doivent être à un canal avec une fréquence d'échantillonnage de 16kHz. Celle-ci est la configuration utilisée dans l'article de wav2vec2.0.
  
```shell script
$ fairseq-hydra-train \
    task.data=/path/to/data \
    --config-dir wav2vec/config/pretraining \
    --config-name wav2vec2_base_librispeech
```  
# 3. Fine-tuning
Pour faire un fine-tuning du modèle, nous recommandons de suivre les étapes listées sur ce Notebook : [Fine-tuning de XLSR-53 sur le Darija](https://github.com/nairaxo/dialectal-voice-clone/blob/main/wav2vec%202.0/xlsr_wav2vec2_darija_finetuning.ipynb).
