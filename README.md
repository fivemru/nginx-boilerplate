# NGINX boilerplate

### Step 0

Install nginx

```
sudo apt update
sudo apt install nginx
```

To enable the service to start up at boot, you can type:

```
sudo systemctl enable nginx
```

### Step 1

Generate Diffie-Hellman keys:

```
sudo openssl dhparam -out /etc/nginx/dhparam.pem 2048
```

### Step 2

Generate selfsigned certs for `default_server`:

```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/nginx/selfsigned-privkey.pem -out /etc/nginx/selfsigned-fullchain.pem
```

### Step 3

Copy all files from this repo to `/etc/nginx/*`.

Set up `/etc/nginx/sites-enabled/site.com.conf`

### Step 4 (optional)

Create the directory for site.com:

```
sudo mkdir -p /var/www/site.com/public
sudo chown -R $USER:$USER /var/www/site.com/public
sudo chmod -R 755 /var/www/site.com
echo "Hello world" > /var/www/site.com/public/index.html
```

### Step 5

Check config and start / restart / reload

```
sudo nginx -t && sudo systemctl start nginx
```

Reload (soft)

```
sudo nginx -t && sudo systemctl reload nginx
```

Restart (hard)

```
sudo nginx -t && sudo systemctl restart nginx
```
