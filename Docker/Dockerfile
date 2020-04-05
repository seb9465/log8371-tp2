# Isntaller net-tools
FROM docker.elastic.co/elasticsearch/elasticsearch:7.6.1
RUN yum install -y wget java-1.8.0-openjdk nmap curl net-tools

# Télécharger et installer l'agent JProfiler
# Unzip et copier dans /user/local
RUN wget http://download-keycdn.ej-technologies.com/jprofiler/jprofiler_linux_11_1_2.tar.gz -P /tmp/ && \
  tar -xzf /tmp/jprofiler_linux_11_1_2.tar.gz -C /usr/local && \
  rm /tmp/jprofiler_linux_11_1_2.tar.gz

# Configurer le path de l'agent JProfiler
ENV JPAGENT_PATH="-agentpath:/usr/local/jprofiler8/bin/linux-x64/libjprofilerti.so=port=8849"
USER elasticsearch

# Exposer les ports de l'agent JProfiler et d'Elasticseach
EXPOSE 8849 9200