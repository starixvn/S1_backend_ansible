# jenkins
docker run -d -v /newvolume/jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 myjenkins:0.7

# artifact
sudo mkdir /newvolume/nexus-data
sudo chown -R 200 /newvolume/nexus-data
sudo docker run -d -v /newvolume/nexus-data:/nexus-data -p 8081:8081 -p 8082:8082 --name nexus sonatype/nexus3

# filebeat
docker run -d -v /logs:/logs -v /usr/share/filebeat/filebeat.yml:/usr/share/filebeat/filebeat.yml docker.elastic.co/beats/filebeat:7.11.1

# nginx
sudo docker run -d -p 80:80 -p 7789:7789 -v /nginx:/etc/nginx -v /usr/share/GeoIP:/usr/share/GeoIP nginx:1.18.0

# cadvisor
sudo docker run \
  --volume=/:/rootfs:ro \
  --volume=/var/run:/var/run:rw \
  --volume=/sys:/sys:ro \
  --volume=/var/lib/docker/:/var/lib/docker:ro \
  --publish=8080:8080 \
  --detach=true \
  --privileged=true \
  --name=cadvisor \
  gcr.io/cadvisor/cadvisor:v0.35.0

# prometheus
docker run -d -v /etc/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml -p 9090:9090 prom/prometheus

# grafana
docker run -d -p 3000:3000 grafana/grafana