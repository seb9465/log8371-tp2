Fichie docker
#####################
1. creer Dockerfile
2. creer docker-compose.yaml

Invite de commande
######################
3. docker build -t <name of your image> . (might work with docker-compose build)c
4. docker network create elasticnetwork
5. docker run -d --name <name of your image> --net elasticnetwork -p 9200:9200
-p 9300:9300 -p 8849:8849 -e "discovery.type=single-node" <name of your image>
6. docker exec -it <name of your image> /bin/bash
7. cd ../usr/local/jprofiler11.1.2/ (ou selon la version)
8. ./bin/jpenable --gui --port=8849

Facultatif supprime un ancien build:
a. docker stop $(docker ps -q) -f
b. docker rm $(docker ps -a -q) -f
c. docker rmi $(docker images -q) -f
d. docker volume prune

JProfiler
#####################
1. New Session
2. Attach -> selectionner (o) Attach to remote jvm
3. set le port 8849 puis faire OK
4. Nouvelle fenetre apparait [Session Startup]
Call-tree recording: Instrumentation
Initial recording profile: CPU Recording
OK
*Vous etes alors en profilage

JMeter
#######################
nb: Notre cas de test se situe sur le dossier .jmx

1.Ouvrir le dossier /bin/ApacheJMeter.jar
2. Dans le dossier Thread group: spécifier les cas de threads: Number of threads, Ramp-up period, Loop Count
3. Dans le dossier CSV Data Set Config: Load metadata.csv
4a).Dans le dossier Query For Test Plan (HTTP Request): Faire un requête POST en spécifiant le path: url/<nom du fichier de donnée>/_search, puis y donner un 
query body. Le query peut etre pas mal n'importe quoi. Un exemple réadapter de ElasticSearch y a été mis
4b). Faire Play sur JMeter/ Start Recording sur Jprofiler
5a).Dans le dossier Query For Test Plan: Faire un requête GET en spécifiant le path: url/<nom du fichier de donnée>/_search, puis y donner un 
query body. Le query peut etre pas mal n'importe quoi. Un exemple réadapter de ElasticSearch y a été mis
5b). Faire Play sur JMeter/ Start Recording sur Jprofiler
6. Todo: Pour augmenter le nombre de requête, il faudra realiser d'autre HTTP Request
 