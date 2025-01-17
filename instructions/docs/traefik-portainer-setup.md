# Traefik and Portainer Installation  

## Introduction  

This guide provides step-by-step instructions for installing Traefik and setting up SSL certificates using Cloudflare and Let’s Encrypt. Additionally, you’ll learn how to install Portainer as a graphical interface for managing your applications.  

## Setting Up Cloudflare  

To begin, ensure you have a Cloudflare account. This guide uses Cloudflare’s free tier, which is ideal for managing DNS and handling SSL certificates.  

1. Register a Domain. If you haven’t already registered a domain, choose a registrar you’re comfortable with.  

2. Add Your Domain to Cloudflare. Update your domain’s nameservers to the ones provided by Cloudflare. Once the domain is active in Cloudflare’s dashboard:  
   - Add A records for both Traefik and Portainer, pointing them to the appropriate server IP address.  
   - Disable proxy and use DNS only.  

3. Create an API Token. You’ll need an API token to manage DNS records programmatically. Follow [this link](https://dash.cloudflare.com/profile/api-tokens) to create one.  

## Updating Port Forwarding  

If you’re using port forwarding to access applications externally, update the `/etc/network/interfaces` file on your Proxmox server:  

1. Open the file for editing:

   ```bash  
   nano /etc/network/interfaces  
   ```  

2. Add the following rules to forward incoming traffic on ports `80` and `443` to the VM running Docker:  

   ```bash  
   # Forward incoming traffic to the Docker VM  
   post-up   iptables -t nat -A PREROUTING -i vmbr0 -s 0.0.0.0/0 -p tcp --dport 80 -j DNAT --to 10.10.10.101:80  
   post-down iptables -t nat -D PREROUTING -i vmbr0 -s 0.0.0.0/0 -p tcp --dport 80 -j DNAT --to 10.10.10.101:80  

   post-up   iptables -t nat -A PREROUTING -i vmbr0 -s 0.0.0.0/0 -p tcp --dport 443 -j DNAT --to 10.10.10.101:443  
   post-down iptables -t nat -D PREROUTING -i vmbr0 -s 0.0.0.0/0 -p tcp --dport 443 -j DNAT --to 10.10.10.101:443  
   ```  

3. Apply the new rules:  

   ```bash  
   ifreload -a  
   ```  

## Installing Docker and Docker Compose  

Since all applications will run in Docker, follow the [official Docker installation guide](https://docs.docker.com/engine/install/ubuntu/) to install Docker and Docker Compose on your Docker VM.  

## Traefik Installation  

1. Log in to the VM hosting Docker:  

   ```bash  
   ssh CustomUserName@server-ip -p [vm-custom-port] -i ~/.ssh/private_key  
   ```  

2. Clone the repository or manually replicate the files from the `docker/traefik` folder:  

   ```bash  
   git clone https://github.com/drozdovilyaa/mvp-playbook.git  
   ```  

3. Update the `.env` file in `docker/traefik` with your environment variables.  

4. Edit the `defaults.yml` file in `docker/traefik/config` to include your IP addresses and `basicAuth` credentials for the Traefik dashboard. Generate hashed passwords using `htpasswd`:  

   ```bash  
   htpasswd -nb username password  
   ```  

   > Since we are forwarding all traffic from ports 80 and 443, it’s crucial to restrict access to internal apps like Traefik and Portainer. Add your IP address to the ipAllowlist middleware configuration in the defaults.yml file. This ensures that only allowed traffic can access these applications.

5. Create a Docker network for Traefik:  

   ```bash  
   sudo docker network create --driver=bridge traefik3-public  
   ```  

6. Start Traefik:

   ```bash  
   sudo docker compose -f docker/traefik/traefik.yml up -d  
   ```  

7. Access your Traefik installation via your web browser.  

## Portainer Installation  

1. Clone the repository or manually replicate the files from the `docker/portainer` folder:

   ```bash  
   git clone https://github.com/drozdovilyaa/mvp-playbook.git  
   ```  

2. Update the `.env` file in `docker/portainer` with your environment variables.  

3. Create a Docker network for Portainer:

   ```bash  
   sudo docker network create --driver=bridge agent-network  
   ```  

4. Start Portainer:  

   ```bash  
   sudo docker compose -f docker/portainer/portainer.yml up -d  
   ```  

5. Open the Portainer dashboard in your web browser and set up your username and password.  
