Multinode vagrant for kubernetes
--------------------------------

Hope it helps start an in-a-laptop (linux) multi-node vagrant platform for a kubernets cluster

#Whats included ?

1. "kuberdeb" // a vagrant packaged virtualbox-ready debian 10 box -including vagrant user, vbox extensions and ssh vagrant insecure key- .... now in vagrant cloud https://app.vagrantup.com/debtano/boxes/kuberdeb/versions/0.0.1
2. Vagrantfile // A multi node -master and 3 working nodes- vagrant file to deploy 4 machines : master, wnode1, wnode2, wnode3
	/*
	* Include inline scripts to setup hosts file, install docker as runtime and kubeadm kubectl and kubelet -and dependencies-
	* Swap should be disable for kubelet to work so an inline script is in charge of that
	*/
3. docker and kubernetes gpg keys for easy apt conf for software installation
4. daemon.json is the recommend docker setup from kubernetes 

#Whats NOT included -yet- ?

pre-setup.sh // Check virtualization HW, install virtualbox 6.0, install vagrant 2.2.5
             // My environment is : 8 gb RAM, core i5, debian 10, vbox 6.0, vagrant 2.2.5

#What is ugly ? |/-)

* I should fix cut & paste code in Vagrantfile, yes, horrible
* Too much inline scripts 
* No parametrization -like required resources, software versions
.....
....help me complete the list ...

#What next

After cloning you should be able to :

1. vagrant status
2. vagrant up (everything or by machine) -will download the box https://app.vagrantup.com/debtano/boxes/kuberdeb/versions/0.0.1
3. vagrant ssh master
4. kubeadm init

..... from there you started the cluster 


