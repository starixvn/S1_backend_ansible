# jenkins
<pre><code>
docker run -d -v /newvolume/jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 --name jenkins myjenkins:0.9
</code></pre>

# artifact
* sudo mkdir /newvolume/nexus-data
* sudo chown -R 200 /newvolume/nexus-data
<pre><code>
sudo docker run -d -v /newvolume/nexus-data:/nexus-data -p 8081:8081 -p 8082:8082 --name nexus sonatype/nexus3
</code></pre>

# filebeat
<pre><code>
docker run -d -v /logs:/logs -v /usr/share/filebeat/filebeat.yml:/usr/share/filebeat/filebeat.yml --user=root --restart always --name filebeat docker.elastic.co/beats/filebeat:7.15.2
</code></pre>

# nginx
<pre><code>
sudo docker run -d -p 80:80 -p 7789:7789 -v /nginx:/etc/nginx -v /usr/share/GeoIP:/usr/share/GeoIP nginx:1.18.0
</code></pre>

# cadvisor
<pre><code>
sudo docker run \
  --volume=/:/rootfs:ro \
  --volume=/var/run:/var/run:rw \
  --volume=/sys:/sys:ro \
  --volume=/var/lib/docker/:/var/lib/docker:ro \
  --publish=8080:8080 \
  --detach=true \
  --restart always \
  --privileged=true \
  --name=cadvisor \
  gcr.io/cadvisor/cadvisor:v0.35.0
</code></pre>

# prometheus
<pre><code>
docker run -d -v /etc/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml -p 9090:9090 prom/prometheus
</code></pre>

# grafana
<pre><code>
docker run -d -p 3000:3000 grafana/grafana:8.2.5
</code></pre>

# redis
### master
<pre><code>
sudo docker run -v /home/centos/redis_master.conf:/etc/redis/redis_master.conf --name redis-master -p 6379:6379 -d redis:6.2.6 redis-server /etc/redis/redis_master.conf
sudo docker run -v /etc/redis/redis_master.conf:/etc/redis/redis_master.conf --name redis-master -p 6379:6379 -d redis:6.2.6 redis-server /etc/redis/redis_master.conf
</code></pre>

### slave
<pre><code>
sudo docker run -v /home/centos/redis_replica.conf:/etc/redis/redis_replica.conf --name redis-slave -p 6379:6379 -d redis:6.2.6 redis-server /etc/redis/redis_replica.conf
sudo docker run -v /etc/redis/redis_replica.conf:/etc/redis/redis_replica.conf --name redis-slave -p 6379:6379 -d redis:6.2.6 redis-server /etc/redis/redis_replica.conf
</code></pre>

### sentinel
* mkdir -p ${PWD}/sentinel_conf
* chmod -R 0777 ${PWD}/sentinel_conf
* chmod 666 ${PWD}/sentinel_conf/redis_sentinel.conf
<pre><code>
sudo docker run -v /home/centos/sentinel1_conf:/sentinel_conf --name redis-sentinel1 -p 26381:26381 -d redis:6.2.6 redis-server /sentinel_conf/redis_sentinel.conf --sentinel
sudo docker run -v /etc/redis/sentinel_conf:/sentinel_conf --name redis-sentinel1 -p 26381:26381 -d redis:6.2.6 redis-server /sentinel_conf/redis_sentinel.conf --sentinel
</code></pre>