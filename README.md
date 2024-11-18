# Repo for the devops related stuff for eng work

- parent repo:

# Steps done:

## Deploy minikube
- Buy Hetzner server
- Add sudo user [tutorial](https://www.digitalocean.com/community/tutorials/how-to-create-a-new-sudo-enabled-user-on-ubuntu)
- Deploy docker using this [tutorial](https://docs.docker.com/engine/install/ubuntu/)
- Deploy minikube using this [tutorial](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fwindows%2Fx86-64%2Fstable%2F.exe+download)
- Important: change minikube RAM to 6GB (I have machine with 8 available)

## Deploy nginx as proxy
Why? Because minikube has one node that is not access-able from internet, so the connection goes like that: internet -> server -> minikube -> k8s svc.
- install nginx: `sudo apt install nginx -y`
- add nginx config file: `sudo vim /etc/nginx/sites-available/reverse-proxy.conf`
- copy contents of nginx-config file inside
- link config: ` sudo ln -s /etc/nginx/sites-available/reverse-proxy.conf /etc/nginx/sites-enabled/`
- restart nginx service: `sudo systemctl restart nginx`

## Deploy postgres
- use this [tutorial](https://www.digitalocean.com/community/tutorials/how-to-deploy-postgres-to-kubernetes-cluster)

## Deploy front-end:
- create namespace front: `kubectl create namespace front`
- apply all files in front-end folder

## Deploy back-end:
- create namespace front: `kubectl create namespace back`
- apply all files in back-end folder

## Setup ELK
ELK - Elasticsearch, Logstash, and Kibana
- based on this [tutorial](https://surajsoni3332.medium.com/setting-up-elk-stack-on-kubernetes-a-step-by-step-guide-227690eb57f4)
- based on this helpful [video](https://www.youtube.com/watch?v=SU--XMhbWoY&t=3s)
