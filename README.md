#dockercoins
```
github_branch=2021-10
github_repository=dockercoins
github_username=amikshas
```

```
git clone https://github.com/amikshas/dockercoins
cd dockercoins/
git checkout 2021-10
```

```
for app in hasher rng webui worker
do 
 docker build --file ${app}/Dockerfile --tag ${github_username}/${github_repository}:${github_branch}-${app} .
done
```

```
for app in hasher redis rng
do
  docker network create ${app}
done
```

```
docker volume create redis
```

```
docker run --detach --name redis --network redis --volume redis:/data:rw library/redis:alpine
docker diff redis
```


```
docker run --detach --entrypoint ruby --name hasher --network hasher --volume ${PWD}/hasher/hasher.rb:/hasher.rb:ro ${github_username}/${github_repository}:${github_branch}-hasher hasher.rb

docker logs hasher
```

```
docker run --detach --entrypoint python --name rng --network rng --volume ${PWD}/rng/rng.py:/rng.py:ro ${github_username}/${github_repository}:${github_branch}-rng rng.py

docker logs rng
```

```
for network in hasher rng 
do
 docker network connect ${network} worker
done

docker network ls
```

```
docker run --detach --entrypoint node --name webui --network redis --publish 8080 --volume ${PWD}/webui/webui.js:/webui.js:ro --volume ${PWD}/webui/files/:/files/:ro ${github_username}/${github_repository}:${github_branch}-webui webui.js

docker logs webui

docker port webup
```
