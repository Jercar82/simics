# Instance Docker

## Configuration
Le mot de passe du compte "operator" ("operator" par défaut) peut être configuré dans le fichier Dockerfile, à la ligne :
```
RUN echo SetEnv OPERATOR_PWD operator >> /etc/apache2/conf-enabled/environment.conf
```
Certaines distribution Linux ne prennet as en compte le compte User
$ 

## Construction
1. Se déplacer dans le dossier $git_simics$/Eolienne/
2. Executer
```
$ docker build -t simics_eolienne .
PS : Le point à la fin de la ligne est trés important
```

## Lancement et récupération de l'adresse IP
### Linux
1. Lance le docker pour qu'il soit en ligne :
$ docker run -it -p 502:502 -p 80:80 eolienne
2. Changer les paramètre de votre port de connexion si le 80 est deja installé sur votre machine.
```
$ DOCKER_ID=$(docker run --rm --detach simics_eolienne)
$ docker inspect --format '{{ .NetworkSettings.IPAddress }}' $DOCKER_ID
```

### Windows

*Note : Docker Desktop for Windows ne permet pas l'exposition des ports. L'exemple suivant permet de lier le port du container avec celui de l'hôte*

```
cmd> for /f "delims=" %i in ('docker run --publish 80:80 --publish 502:502 --rm --detach simics_eolienne') do set DOCKER_ID=%i
cmd> docker inspect --format='{{.NetworkSettings.IPAddress}}' %DOCKER_ID%
```

## Suppression
```
$ docker rmi simics_eolienne
```
