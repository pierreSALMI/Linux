# TP-HTTP

## Config Apache

Pour modifier le nom de domaine en `wiki.lab.local` il faut configurer le fichier `httpd.conf` 

## Reverse Proxy NGINX

On créé une troisieme VM `Proxy` sur laquelle on installe `nginx` et configure `nginx.conf`

`apt-get install -y nginx`

```
upstream big_server_com {
    server 192.168.56.11:80;
    server 192.168.56.12:80;
  }

  server {
    listen          80;
    server_name     wiki.lab.local;
    access_log      logs/wiki.lab.access.log main;

    location / {
      proxy_pass      http://big_server_com;
    }
  }
}
```