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

fichier de configuration au demarrage dans /etc/logstash/conf.d

mkdir /opt/logstash/patterns

cd /opt/logstash/patterns

wget

chown -R logstash:logstash /opt/logstash/patterns


[voir](https://github.com/Grosloup/tuto-elk-howto/blob/master/logstash.conf) config à améliorer

###Lancer/arreter/status/redemarrage

service logstash start|stop|status|restart

##Installation d'elasticsearch

###Installation des sources

(au besoin : apt-get install python-software-properties)

add-apt-repository "deb http://packages.elasticsearch.org/elasticsearch/1.4/debian stable main"

dans /etc/apt/sources.list retirer la ligne deb-src d'elasticsearch

###Installation d'elasticsearch

apt-get update && apt-get install elasticsearch

###Lancer elasticsearch au boot

update-rc.d elasticsearch defaults 95 10

###Lancer/arreter/status/redemarrage

service elasticsearch start|stop|status|restart

##Installation de kibana

cd /var/www

wget https://download.elastic.co/kibana/kibana/kibana-4.0.2-linux-x64.tar.gz

tar xvf kibana-4.0.2-linux-x64.tar.gz

mv kibana-4.0.2-linux-x64.tar.gz kibana

##Création d'un vhost (nginx)

wget https://raw.githubusercontent.com/Grosloup/tuto-elk-howto/master/kibana.conf -O /etc/nginx/sites-available/kibana.conf

modifier kibana.conf (server_name...), créer les fichiers de log, protéger le répertoire...

mkdir /var/log/nginx/kibana

touch /var/log/nginx/kibana/access.log

touch /var/log/nginx/kibana/error.log

chown -R www-data:www-data /var/log/nginx/kibana

ln -s /etc/nginx/sites-available/kibana.conf /etc/nginx/sites-enabled/

service nginx reload

###Lancer kibana au boot

cd /etc/init.d && wget https://gist.githubusercontent.com/thisismitch/8b15ac909aed214ad04a/raw/bce61d85643c2dcdfbc2728c55a41dab444dca20/kibana4

modifier kibana4 (chemin vers bin/kibana)

chmod +x /etc/init.d/kibana4

update-rc.d kibana4 defaults 96 9

###Lancer/arreter/status/redemarrage

service kibana4 start|stop|status|restart

