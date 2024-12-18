# Repo for the devops related stuff for eng work

- parent repo:

# Steps done:

## Deploy minikube
- Buy Hetzner server
- Add sudo user [tutorial](https://www.digitalocean.com/community/tutorials/how-to-create-a-new-sudo-enabled-user-on-ubuntu)
- Deploy docker using this [tutorial](https://docs.docker.com/engine/install/ubuntu/)
- Deploy minikube using this [tutorial](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fwindows%2Fx86-64%2Fstable%2F.exe+download)
- Important: change minikube RAM to 12GB (I have machine with 16 available)

## Deploy nginx as proxy
Why? Because minikube has one node that is not access-able from internet, so the connection goes like that: internet -> server -> minikube -> k8s svc.
- install nginx: `sudo apt install nginx -y`
- add nginx config file: `sudo vim /etc/nginx/sites-available/reverse-proxy.conf`
- copy contents of nginx-config file inside
- link config: ` sudo ln -s /etc/nginx/sites-available/reverse-proxy.conf /etc/nginx/sites-enabled/`
- restart nginx service: `sudo systemctl restart nginx`

## Deploy postgres
- use configs in postgres config according to this [tutorial](https://www.digitalocean.com/community/tutorials/how-to-deploy-postgres-to-kubernetes-cluster)
- set val_level to logical to support pg_sync
    - log on postgres pod:

        `kubectl exec -it postgres-dbfd84ff5-62hxs -n default -- psql -h localhost -U postgres --password -p 5432`
    - run in postgres:

        `ALTER SYSTEM SET wal_level = logical;`
        `ALTER SYSTEM SET max_replication_slots = 5;` # has to at least one

        `SELECT pg_reload_conf();`

    - restart deployment:

        `kubectl rollout restart deployment postgres -n default`
    - after restart you can check with:

        `SHOW wal_level;`
        `SHOW max_replication_slots;`

## Deploy front-end:
- create namespace front: `kubectl create namespace front`
- apply all files in front-end folder

## Deploy back-end:
- create namespace front: `kubectl create namespace back`
- apply all files in back-end folder

## Setup ELK
ELK - Elasticsearch, Logstash, and Kibana
- based on this helpful [video](https://www.youtube.com/watch?v=SU--XMhbWoY&t=3s)
