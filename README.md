# dockercoins
...
github_branch=2021-10
github_repository=dockercoins
github_username=amikshas
...

# git clonehttps://github.com/amikshas/dockercoins
# cd dockercoins/
# git checkout 2021-10
...

...
for app in hasher rng webui worker
do 
 docker build --file ${app}/Dockerfile --tag ${github_username}/${github_repository}:${github_branch}-${app}
done
...
