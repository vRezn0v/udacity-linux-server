# Udacity Full Stack Nanodegree Linux Server Configuration

The final project for Udacity Fullstack Nanodegree. An Amazon Lightsail instance running ubuntu, to host the [Item Catalog App](https://github.com/vRezn0v/foss-catalog).

Server IP:
```
15.206.129.232
```
SSH Port:
```
2200
```
The Catalog Web App can be accessed from ```http://15.206.129.232/catalog/```

### Accessing via SSH:
``` $ ssh -i <key>.rsa grader@15.206.129.232 -p 2200```

### Installation Summary:
An Amazon LightSail Instance was created and allocated a static IP from AWS dashboard, the ssh keys were acquired for first time access. A new user was created for user ```grader``` with ability to sudo and a home directory. Fresh SSH keys were generated for grader and local timezone was set to UTC.
#### Software (packages) Installed:
- Apache2
- python-setuptools
- libapache2-mod-wsgi
- python-psycopg2
- Postgresql
- Git
- python dependencies from Catalog App
### Configuration Changes:
- SSH Port changed to 2200 from 22 for security by editing ```/etc/ssh/sshd_config``` and restarting the service.
- UFW configured and enabled to only allow TCP traffic on ports 2200 and 80 (SSH and HTTP) and UDP on 123.
- Amazon Firewall reconfigured to allow above mentioned ports only.
- Postgresql was configured with a new username ```fosscatalog``` and respective database was created to be used with Catalog App. And remote connections were verified to be disabled.
- The Catalog App repository was cloned into ```/var/www```, the main file ```catalog.py``` renamed to ```__init__.py``` and every instance of ```sqlite://catalog.db``` was replaced with ```postgresql://fosscatalog:password@localhost/fosscatalog``` to use postgresql server instead of a sqlite database.
- ```FlaskApp.conf``` was generated for catalog app and the app was enabled for use with Apache using ```a2ensite```. and Web Service Gateway Interface (WSGI) configured  for FlaskApp (Catalog).

### Resources:
- [DigitalOcean Tutorial on hosting Flask App on Apache](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps)
- [Using Postgresql with SQLAlchemy](https://www.compose.com/articles/using-postgresql-through-sqlalchemy/)
- [DigitalOcean UFW Essentials](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands)
