# Wallhack lan

These compose-files are used for deploying gameserver-stacks on docker-swarm with a macvlan network.


## Install macvlan in docker-swarm

1. First create a config only net on all nodes (Thank you ansible) 


`$ docker network create --config-only --subnet 10.50.1.0/24 -o parent=eth0.50 --ip-range 10.50.1.2/24 confignet`

2. Create macvlan on master node


`$ docker network create -d macvlan --scope swarm --config-from confignet swarm-macvlan`

3. Deploy stack

`$ docker stack deploy -c csgo.yml`
