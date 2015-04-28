#ELK pour Elasticsearch Logstash Kibana

##Installation de java

###Installation des sources

echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee /etc/apt/sources.list.d/webupd8team-java.list

echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list

apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886

###Installation de java

apt-get update && apt-get install oracle-java8-installer

##Installation de logstash

###Installation des sources

wget -qO - https://packages.elasticsearch.org/GPG-KEY-elasticsearch | sudo apt-key add -

echo 'deb http://packages.elasticsearch.org/logstash/1.5/debian stable main' | sudo tee /etc/apt/sources.list.d/logstash.list

###Installation de logstash

apt-get update && apt-get install logstash

###Lancer logstash au boot

update-rc.d logstash defaults 95 10

##Installation d'elasticsearch

###Installation des sources

(au besoin : apt-get install python-software-properties)

add-apt-repository "deb http://packages.elasticsearch.org/elasticsearch/1.4/debian stable main"

dans /etc/apt/sources.list retirer la ligne deb-src d'elasticsearch

###Installation d'elasticsearch

apt-get update && apt-get install elasticsearch

###Lancer logstash au boot

update-rc.d elasticsearch defaults 95 10
