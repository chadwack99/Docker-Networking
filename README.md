# Docker-Networking
Keeping the info learned on Docker networking

Working with ipvlans in docker is pretty cool.


Create new ipvlan:
docker network create -d ipvlan --subnet 0.0.0.0/24 -o parent=host_nic_name -o ipvlan_mode=l3 ipvlan_name # must add all the subnets that will be sharing the host nic docker will work it's magic.

Assinging the network to a container next:
Test web server:
docker run -itd --rm --network ipvlan_name --ip 0.0.0.2/24 --name webserver1 nginx:latest

Next need to add the route in your firewall or top of rack L3 switch to point to the IP of the VM_host IP the new ipvaln was made on. The host will know what to do with the traffic.

