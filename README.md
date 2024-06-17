# kong-hybrid-setup

docker-compose -f cp.yaml up -d

docker-compose -f dp.yaml up -d

**docker exec into control plane**

apt-get update

apt-get install nano

kong hybrid gen_cert

cp /etc/kong/kong.conf.default /etc/kong/kong.conf

nano /etc/kong/kong.conf

set role = control_plane

set cluster_cert=/cluster.crt

set cluster_key=/cluster.key

kong reload

kong restart

**docker exec into data plane**

apt-get update

apt-get install nano

copy same cluster crt and key from control plane

cp /etc/kong/kong.conf.default /etc/kong/kong.conf

nano /etc/kong/kong.conf

set role = data_plane

set cluster_cert=/cluster.crt

set cluster_key=/cluster.key

set cluster_control_plane=control-plane:8005 		#control-plane is name of the kong control plane docker container 

kong reload

kong restart
