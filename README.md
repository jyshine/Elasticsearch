# Elasticsearch

Oracle VM VritualBox 6.0.
Ubuntu 18.0.041 (64bit)
Elasticsearch-6.4.2 deb
Kibana-6.4.2-amd64.deb
Logstash-6.4.2.deb
Filebeat-6.4.2-amd64.deb


sudo apt-get update
sudo dpkg --configure -a

기본툴 설치
	gedit설치
		sudo apt-get install gedit
	net-tools 설치
		sudo apt install net-tools
	curl 설치
		sudo apt-get install curl


서버 설치
	Apache(아파치) 서버
		sudo apt-get install apache2
JAVA 설치
	sudo add-apt-repository ppa:webupd8team/java
	sudo apt-get update	
	//sudo apt-get install oracle-java8-installer
	sudo apt install openjdk-8-jdk openjdk-8-jre
	
Elasticsearch 설치
	wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.4.2.deb
Kibana 설치
	wget https://artifacts.elastic.co/downloads/kibana/kibana-6.4.2-amd64.deb
Logstash 설치
	wget https://artifacts.elastic.co/downloads/logstash/logstash-6.4.2.deb
Filebeat 설치
	wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-6.4.2-amd64.deb

설치 파일 확인
	ls

Elasticsearch
	설치
		sudo dpkg -i elasticsearch-6.4.2.deb
	서비스 등록
		sudo systemctl enable elasticsearch.service
	서비스 실행 및 실행여부 확인
		sudo service elasticsearch start
		curl -XGET "localhost:9200"
			결과 오류 :curl: (3) Port number ended with '�'
			해결 : 포트 열어줌
				sudo ufw allow 9200
Logstash		
	sudo dpkg -i logstash-6.4.2.deb
Kibana
	sudo dpkg -i kibana-6.4.2-amd64.deb
	
	설정
	sudo gedit /etc/kibana/kibana.yml 
	
	#elasticsearch.url: "https://localhost:9200"
	#server.host: "localhost"
Filebeat
	sudo dpkg -i filebeat-6.4.2-amd64.deb
	설정
	sudo gedit /etc/filebeat/filebeat.yml
	
	  # Change to true to enable this input configuration.
	  #enabled: false
	  enabled: true
	  
	    # Paths that should be crawled and fetched. Glob based paths.
		paths:
			- /var/log/*.log
			- /var/log/syslog
			- /var/log/apache2/*.log

sudo service apache2 stop
sudo service elasticsearch stop
sudo service kibana stop
sudo service filebeat stop

sudo service apache2 start
sudo service elasticsearch start

curl -XGET "localhost:9200"

sudo service kibana start
sudo service filebeat start

확인
filebeat 
	127.0.0.1:9200/_cat/indices
Kinaba
	127.0.0.1:5601
	
