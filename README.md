### Section Docker

Pour build l'image, la push sur DockerHub, il faut réaliser les commandes ci-dessous (en partant du principe que l'on est dans l'emplacement du fichier Dockerfile): 

```bash
docker build -t samir1977/exo05-api:latest .
docker login
docker push samir1977/exo05-api:latest
```

Si l'on veut la tester, on peut le faire via la commande suivante: 

```bash
docker run --name exo05-api -p 3000:80 -d exo05-api
```

---

### Section K8s

Pour pouvoir lancer notre image sur Kubernetes, il nous faut avoir un cluster. Dans notre cas, nous utiliserons minikube:

```bash
minikube start --driver docker
```

Puis il va nous falloir appliquer nos fichiers de ressources à notre cluster pour changer son état et permettre:

* La création dans les nodes de nos pods faisant tourner les conteneurs avec notre image
* La création d'un service de type **LoadBalancer** permettant d'atteindre l'une des 5 replicas en cas de crash / restart de l'un de nos pods.
* declarer la variable d'environnement STORY_FOLDER en lui attribuant le chemin du fichier /story qui va contenir l'histoire

```bash
kubectl apply -f .\ressources-files\deployment.yml,.\ressources-files\service.yml
minikube service dotnet-app-service
```

Il ne nous reste plus qu'a essayer d'atteindre l'endpoint **/WeatherForecast** de notre API via l'adresse générée par minikube de cette route.

---
Pour réaliser un POST vers /story d'un JSON

* Télécharger et installer Postman .

* Dans l'interface de Postman, sélectionner le type de requête HTTP (GET, POST, PUT...) à envoyer. Pour un POST, sélectionner "POST".

* Indiquer l'URI dans la barre d'adresse, en l'occurrence "/story" pour ce cas précis.

* Ajouter les éventuels paramètres à passer avec l'URL dans la section "Params". Pour ce cas précis, il n'y a pas de paramètres à ajouter.

* Ajouter les headers nécessaires à la requête. Pour formuler une requête, le header n'est utilisé qu'avec PUT (mise à jour) ou POST (création). Il contient les informations supplémentaires sur le message. Les headers sont représentés par une paire clé et valeur, et il existe de nombreux types d’options différents pour eux. Par exemple : Utilisateur-Agent : Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_5). Vous pouvez consulter la liste complète des différentes options pour les headers [1].

* Ajouter le body de la requête. Le body contient les données réelles de la ressource que vous essayez de créer ou de mettre à jour. Les données sont envoyées sous format JSON. Pour ajouter les détails de l'utilisateur (prénom, nom, adresse...) dans le body, en JSON, il faut sélectionner l'onglet "Body" et choisir l'option "raw". Ensuite, il faut sélectionner le format "JSON" et ajouter le JSON dans le champ de texte .


![Smiling Dog](https://s.abcnews.com/images/Lifestyle/HT_Herbert_Smiling_Dog_2_ER_160113_16x9_992.jpg)