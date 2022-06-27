Setup the environment

multipass launch --network name=bridge0 --mount /home/manuel/Downloads/:/mnt/Downloads/ --name couchbase-db-1 22.04
sudo snap install lxd
multipass set local.driver=lxd
sudo snap connect multipass:lxd lxd
multipass set local.bridged-network=wlp2s0
multipass launch --bridged  --name couchbase-db-1 22.04

multipass mount /home/manuel/Downloads/ couchbase-db-1:/mnt/Downloads/
multipass mount /home/manuel/Downloads/ couchbase-db-2:/mnt/Downloads/
multipass mount /home/manuel/Downloads/ couchbase-db-3:/mnt/Downloads/
multipass exec couchbase-db-1 -- sudo apt update 
multipass exec couchbase-db-1 -- sudo apt install libtinfo5
multipass exec couchbase-db-1 -- sudo dpkg -i /mnt/Downloads/couchbase-server-community_7.1.0-ubuntu20.04_amd64.deb

multipass exec couchbase-db-2 -- sudo apt update 
multipass exec couchbase-db-2 -- sudo apt install -y libtinfo5
multipass exec couchbase-db-2 -- sudo dpkg -i /mnt/Downloads/couchbase-server-community_7.1.0-ubuntu20.04_amd64.deb

multipass exec couchbase-db-3 -- sudo apt update 
multipass exec couchbase-db-3 -- sudo apt install -y libtinfo5
multipass exec couchbase-db-3 -- sudo dpkg -i /mnt/Downloads/couchbase-server-community_7.1.0-ubuntu20.04_amd64.deb
