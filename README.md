<p align="center">
  <img src="https://github.com/AIOXLABS/DVoice/blob/main/logo.jpeg" width="350" alt="logo">
</p>

# 1. A propos
Basée à Rabat, Londres et Paris, AIOX-Labs mobilise les technologies d’intelligence artificielle pour répondre aux besoins métiers et projets data des entreprises.
- Au service de la croissance des groupes, de l’optimisation des processus ou de l’amélioration de l'expérience client.
- AIOX-Labs est multisecteur, de la fintech à l’industrie en passant par le retail et les biens de consommation.
- Des data products business ready avec un socle algorithmique solide et une adaptabilité pour les besoins spécifiques de chaque client.
- Une équipe complémentaire composée de docteurs en IA et d’experts métiers avec une assise scientifique solide et des publications internationales.

Site web : https://www.aiox-labs.com/

Dialectal Voice est un projet communautaire initié par AIOX-Labs pour faciliter la reconnaissance de la voix par les Systèmes Intelligents. Aujourd'hui, le besoin en Systèmes IA capable de reconnaître la voix humaine s'exprime de plus en plus au sein des communautés. On remarque cependant que pour certaines langues comme le Darija, il n'existe pas assez de solutions de technologie vocale. Pour répondre à ce besoin, on s'est proposé alors d'établir ce programme de construction itérative et intéractive d'une base de données dialectale et ouverte à tous afin d'aider à améliorer les modèles de reconnaissance et de génération de la voix.

Sites web : https://dvoice.ma/, https://dvoice.sn/

# 2. Contribuer au projet Dvoice
Il existe deux manières de contribuer au projet:
## 2.1. Soumettre des enregistrements "هضر"
Pour aider à améliorer les technologies vocales sur l’arabe dialectal marocain, il est nécessaire d’avoir une quantité importante de données pour l’entraînement des modèles. Les données se présentent sous forme de « voix + transcription textuelle ». La contribution à l’enrichissement de la dataset se fait par la lecture d’un texte Darija affiché à l’écran suivie de la soumission de l’enregistrement.

N.B : Au moment de la lecture des textes, veuillez vous assurer que votre micro fonctionne parfaitement et qu’il n’y a pas beaucoup de bruits de fond. 

## 2.2. Évaluer des enregistrements "سمع"
Une autre manière de contribuer à cette initiative, c’est d’évaluer des enregistrements. Il s’agit ici d’écouter un échantillon « voix + transcription textuelle » et de l’évaluer en fonction de la proximité entre la voix enregistrée et le texte correspondant. Lorsqu’on juge les deux assez proches, on clique sur « Oui » sinon ça sera « Non ».

# 3. Obtenir la dataset
## 3.1. Dvoice-v1.0
La base de données construite est ouverte au publique. Son acquisition se fait sous deux différentes manières:
- Après souscription sur ce site. On vous l'enverra par suite par mail dans un bref délai.
- En allant sur le répertoire Zenodo depuis ce lien : [Télécharger ici](https://zenodo.org/record/5482551).

## 3.2. Dvoice-v2.0
Cette deuxième version de la dataset, disponible [ici](https://zenodo.org/record/6342622), intègre les données augmentées, facilement repérables et une dataset swahilie obtenue par transfer learning depuis la dataset multilingue [VoxLingua107](http://bark.phon.ioc.ee/voxlingua107/).

N.B : Pour être informé lorsqu'une nouvelle mise à jour de la base de données sera disponible, vous pouvez vous souscrire depuis la page Souscription.

## 3.2. Dataset alternative
L'entraînement d'un modèle de reconnaissance vocale nécessite souvent d'avoir d'une part un ensemble d'enregistrements vocales et d'une autre part leurs transcriptions en texte. L'initiative Dvoice vise justement à pourvoir à la communauté ces prérequis afin de mieux faciliter l'adoption des technologies vocales et la recherche autour d'elles.

Une méthode alternative consiste à faire du transfert learning sur des enregistrements en transcrivant ces dernières en texte. On procède comme suit:
- Récupérer du contenu vidéo public sur Youtube, Facebook,...
- Convertir les vidéos en audios.
- Segmenter les audios obtenus (faire une segmentation par silence).
- Effectuer un pre-processing sur ces données (réduire les bruits, ajouter du silence si nécessaire,...).
- Labelliser les audios avec la bibliothèque [SpeechRecognition](https://pypi.org/project/SpeechRecognition/)

# 4. Notre vision pour DVoice Africa
La plus grande nouveauté de cette première mise à jour du projet DVoice est certainement l'inclusion d'autres langues africaines, un pas important vers l'objectif ultime de ce projet. Aujourd'hui, le projet comprend, au niveau de la collection de données, le Darija puis, via DVoice Senegal, supporte six langues et dialectes (Wolof, Serere, Diola, Mandingue, Pular, Soninke) parlées au Sénégal et dans plusieurs pays d'Afrique de l'Est. Au niveau modèle, il supporte le Darija et le Swahili.

Les premières versions des modèles testés ont de très bons scores. Nous encourageons vivement tout le monde à participer à ce programme communautaire en visitant notre site [Dvoice.ma](https://dvoice.ma/) mais aussi le tout nouveau [Dvoice.sn](https://dvoice.sn/) pour proposer ou valider quelques enregistrements. Celà aidera considérablement à la construction d'une grande base de données vocale africaine.

De notre part on essaie encore d'aller plus loin en accentuant sur des potentiels paramètres/approches à embarquer et sur la possibilité d'intégrer un modèle de langage qui permettra de mieux affiner les transcriptions. L'idée ensuite est de mettre au point et de facilitier les technologies vocales pour les langues africaines.
