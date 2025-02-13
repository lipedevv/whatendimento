[![en](https://img.shields.io/badge/lang-en-green.svg)](README.md)
[![pt-br](https://img.shields.io/badge/lang-pt--br-red.svg)](README.pt.md)

# About the Project

Whatendimento is a communicator with CRM and helpdesk features that utilizes WhatsApp as a means of communication with clients.


Very Quick Start on a public Server
-----------------------------------

There are Docker images provided from the project, so you can get **ticketz** to work very easily on a public server (baremetal or VPS).

### First setup

Before starting you must complete this checklist:

- [X] Have a clean server running Ubuntu 20 or newer
- [X] Ports 80 and 443 available and not filtered by firewall
- [X] One hostname with configured DNS pointing to your server

After this, just log in to your server and issue the following command, replacing the hostnames you already configured and your email address:

```bash
curl -sSL get.ticke.tz | sudo bash -s app.example.com name@example.com
```

After a few minutes you will have the server running at the hostname you defined.

The default login will be the email address provided in the installation command and the default password is `123456`, you must change it right away.

### Upgrade

The upgrade is just easy as the instalation, you just need to login to your server using the same username you used on the installation and issue the following command:

```bash
curl -sSL update.ticke.tz | sudo bash
```

Your server will go down and after some minutes it will be running in the latest released version.

### Inspect logs

As all elements are running in containers the logs must be checked through the docker command.

You must login to your server using the same user you used for the installation.

First you need to move the current directory to the installation folder:

```bash
cd ~/ticketz-docker-acme
```

After this you can get a full log report with the following command:

```bash
docker compose logs -t
```

If you want to "tail follow" the logs just add a `-f` parameter to that command:

```bash
docker compose logs -t -f

```

Running from Source code Using Docker
-------------------------------------

For installation, you need to have Docker Community Edition and the Git client installed. It is ideal to find the best way to install these resources on your preferred operating system. [The official Docker installation guide can be found here](https://docs.docker.com/engine/install/).

In both cases, it is necessary to clone the repository, then open a command terminal:

```bash
git clone https://github.com/allgood/ticketz.git
cd ticketz
```

## Running Locally

By default, the configuration is set to run the system only on the local computer. To run it on a local network, you need to edit the `.env-backend-local` and `.env-frontend-local` files and change the backend and frontend addresses from `localhost` to the desired IP, for example, `192.168.0.10`.

To run the system, simply execute the following command:

```bash
docker compose -f docker-compose-local.yaml up -d
```

On the first run, the system will initialize the databases and tables, and after a few minutes, Ticketz will be accessible through port 3000.

The default username is `admin@ticketz.host`, and the default password is 123456.

The application will restart automatically after each server reboot.

Execution can be stopped with the command:

```bash
docker compose -f docker-compose-local.yaml down
```

## Running and Serving on the Internet

Having a server accessible via the internet, it is necessary to adjust two DNS names of your choice, one for the backend and another for the frontend, and also an email address for certificate registration, for example:

* **backend:** api.ticketz.example.com
* **frontend:** ticketz.example.com
* **email:** ticketz@example.com

You need to edit the `.env-backend-acme` and `.env-frontend-acme` files, defining these values in them.

If you want to use reCAPTCHA in the company signup, you also need to insert the secret and site keys in the backend and frontend files, respectively.

This guide assumes that the terminal is open and logged in with a regular user who has permission to use the `sudo` command to execute commands as root.

Being in the project's root folder, execute the following command to start the service:

```bash
sudo docker compose -f docker-compose-acme.yaml up -d
```

On the first run, Docker will compile the code and create the containers, and then Ticketz will initialize the databases and tables. This operation can take quite some time, after which Ticketz will be accessible at the provided frontend address.

The default username is the email address provided on the `.env-backend-acme` file and the default password is 123456.

The application will restart automatically after each server reboot.

To terminate the service, use the following command:

```bash
sudo docker compose -f docker-compose-acme.yaml down
```

Important Notice
----------------

This project is not affiliated with Meta, WhatsApp, or any other company. The use of the provided code is the sole responsibility of the users and does not imply any liability for the author or project collaborators.

Made Your Life Easier?
----------------------

If this project has helped you with a complex task, consider making a donation to the author via PayPal or Brazilian PIX below.

[![](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=X6XHVCPMRQEL4)

![image](https://github.com/ticketz-oss/ticketz/assets/6070736/8e85b263-73ca-4fb4-9bdc-03fff356b6ff)

PIX Key: 0699c69d-0951-4686-a5b7-c6cd21aa7e15
