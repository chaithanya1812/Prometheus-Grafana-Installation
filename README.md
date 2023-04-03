# Prometheus & Grafana-Installation
![architecture](https://user-images.githubusercontent.com/111736742/229615136-8b17b01b-9695-4133-98ab-46b95029ba6c.png)

#1)----Prometheus Installation
```bash
yum update -y

wget https://github.com/prometheus/prometheus/releases/download/v2.37.6/prometheus-2.37.6.linux-amd64.tar.gz

sha256sum prometheus-2.37.6.linux-amd64.tar.gz

tar -xvzf prometheus-2.37.6.linux-amd64.tar.gz

cd prometheus-2.37.6.linux-amd64
  
vi 
#you can see the some data just leave it as its
 #To start Prometheus excute below command
./prometheus  --config.file=./prometheus.yml &
#Goto Browser
publicip:9090
```
# Prometheus Installation Sucessfull
![prom](https://user-images.githubusercontent.com/111736742/229612904-65a3d2be-61bd-46a9-a927-a79b675d51e8.png)

#---------------------------------------
# Grafana Installation
```bash
vi  /etc/yum.repos.d/grafana.repo
#add below data to /etc/yum.repos.d/grafana.repo
-----------------
[grafana]
name=grafana
baseurl=https://rpm.grafana.com
repo_gpgcheck=1
enabled=1
gpgcheck=1
gpgkey=https://rpm.grafana.com/gpg.key
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
---------------------
exclude=*beta*

yum install grafana

systemctl daemon-reload
systemctl start grafana-server
systemctl status grafana-server

#Goto Browser
publicip:3000
```
![grafana](https://user-images.githubusercontent.com/111736742/229613839-0b3b724c-66a5-4cad-a722-72c211e7487a.png)
# ------------------------
# node-exporter installation
```bash
wget https://github.com/prometheus/node_exporter/releases/download/v1.5.0/node_exporter-1.5.0.linux-amd64.tar.gz
tar -xvzf nod*
cd node_exporter-1.5.0.linux-amd64
./node_exporter &
#Goto Browser
publicip:9100
```
![node-exporter](https://user-images.githubusercontent.com/111736742/229614745-d11572e0-fed1-4f81-95c2-98d97d2c46ac.png)

# How to add targets to Prometheus Server

step1- open vi prometheus.yml 

step2- Add below data
```bash
- job_name: "node-1"

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["3.110.133.111:9100"]
```
 #if you add another node-exporter same you have repeat!!!
 ```bash
- job_name: "node-2"

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["13.233.32.106:9100"]
```
# After adding node-exporters details how its look in (prometheus.yml) file.
![final image](https://user-images.githubusercontent.com/111736742/229617028-a8bf0d07-7e1f-4bc9-973b-83a2d4f90149.png)
# Next  go to prometheus dashboard under Status section select Targets you can see our 2-node exporters details
![prometheusfinal status](https://user-images.githubusercontent.com/111736742/229618621-a182771f-2f8a-4ac9-84c8-ae52a2fe29d6.png)
![png](https://user-images.githubusercontent.com/111736742/229618808-5edd8ae0-f244-4d5f-870f-192ff70a6273.png)



