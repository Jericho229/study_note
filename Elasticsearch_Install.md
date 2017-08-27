# Elasticsearch Init

> Version 5.x

> Ubuntu 16.04

> [Doc] (https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html)

>[Reference] (https://www.elastic.co/guide/en/elasticsearch/reference/5.3/deb.html#deb-repo)

### Install

* Update resources list

	```
	sudo apt-get update
	```

* Install java

	```
	sudo apt-get -y install openjdk-8-jdk openjdk-8-jre
	or
	sudo apt-get -y install openjdk-8-jre ???
	```


* Download and install the public signing key:

	```
	wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
	
	```

* Installing from the APT repositoryedit

	You may need to install the apt-transport-https package on Debian before proceeding:
	
	```
	sudo apt-get install apt-transport-https
	```
	Save the repository definition to /etc/apt/sources.list.d/elastic-5.x.list:
	
	```
	echo "deb https://artifacts.elastic.co/packages/5.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-5.x.list
	```

* Install the Elasticsearch Debian package with:
	
	```
	sudo apt-get update && sudo apt-get install elasticsearch
	```

### SysV init vs systemdedit
Elasticsearch is not started automatically after installation. How to start and stop Elasticsearch depends on whether your system uses SysV init or systemd (used by newer distributions).

```
ps -p 1
```

Running Elast
cㄨsearch with SysV initedit
Use the update-rc.d command to configure Elasticsearch to start automatically when the system boots up:

```
sudo update-rc.d elasticsearch defaults 95 10
```

### Test
```
curl -X GET 'http://localhost:9200'
```


