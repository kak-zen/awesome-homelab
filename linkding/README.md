[Website](https://linkding.link/)
[GitHub](https://github.com/sissbruecker/linkding)
[Demo](https://demo.linkding.link/login/)
[Documentation](https://linkding.link/installation/#using-docker)

Category: Bookmark Manager
Required RAM: 200MB 

### Setup

```mkdir linkding```

```cd linkding```

```nano docker-compose.yml```

Paste the below yml file

<!DOCTYPE html>
<html lang="en">
<body>

<pre>
services:
  linkding:
    container_name: linkding
    image: sissbruecker/linkding:latest
    ports:
      - 9090:9090
    volumes:
      - ./data:/etc/linkding/data
    restart: unless-stopped
</pre>

</body>
</html>

	
To save, press Ctrl O 
To exit, press Ctrl X

That is it. Now, you can run the container with

```docker compose up -d```

Congrats, your container is up successfully. Next, you want to create an admin user. Run the below command, and provide username and an email ID. 

<!DOCTYPE html>
<html lang="en">
<body>

<pre>
docker exec -it linkding bash -c 'read -p "Enter username: " username; read -p "Enter email: " email; python manage.py createsuperuser --username="$username" --email="$email"'
</pre>

</body>
</html>


### Access over the internet

Next is to make linkding online. 

- Go to your [Cloudflare One Dash](https://one.dash.cloudflare.com). 
- Go to Networks - Tunnels 
- Select your tunnel and click on edit. 
- Go to Published application routes
- Click on Add a Published application route
- Fill the details 
	- Subdomain can be linkding
	- select your domain
	- select service type http
	- add url ```localhost:9090```

See the example below

![linkding.png](https://github.com/leonalAbel/cdn/blob/main/public/2025-11-06/cloudflare-linkding.png?raw=true)

- Click on save
- Go to the website
- Set a strong password 

You don't have to remember all your passwords. [Use Vaultwarden to generate and save passwords securely](/blog/selfhost-vaultwarden). 

### Backup your data

There are two ways to backup your data. 
1. Just backup the linkding folder
2. Use crontab to automate backups

### Stop the container

If you want to stop the container, go to the same folder and do

```docker compose down```