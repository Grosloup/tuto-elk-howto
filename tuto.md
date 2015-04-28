#ELK pour Elasticsearch Logstash Kibana

##installation de java

###installation des sources

echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee /etc/apt/sources.list.d/webupd8team-java.list

echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list

apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886

###installation de java

apt-get update && apt-get install oracle-java8-installer

##installation de logstash

###installation des sources

wget -qO - https://packages.elasticsearch.org/GPG-KEY-elasticsearch | sudo apt-key add -

echo 'deb http://packages.elasticsearch.org/logstash/1.5/debian stable main' | sudo tee /etc/apt/sources.list.d/logstash.list

###installation de logstash

apt-get update && apt-get install logstash

###Lancer logstash au boot

update-rc.d logstash defaults 95 10

