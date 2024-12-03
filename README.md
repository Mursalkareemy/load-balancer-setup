# Load Balancer Setup for Assignment 3, Part 2

This repository contains all the necessary files and instructions for setting up a load balancer with two web servers, as required for Assignment 3, Part 2.

## Project Overview

The setup involves:
- Configuring two web servers running Nginx.
- Dynamically generating an `index.html` file using a custom script.
- Serving files via an auto-indexed `/documents/` directory.
- Setting up a DigitalOcean load balancer to route traffic between the two servers.

---

## Repository Contents

- **`generate_index`**:
  - A Bash script to dynamically create an `index.html` file displaying server-specific system information.
- **`index.html`**:
  - A sample HTML file that serves as the main page for each server.
- **`server-block.conf`**:
  - Nginx configuration file for serving the `index.html` file and enabling auto-indexing for `/documents/`.

---

## Setup Instructions

Follow these steps to replicate the setup:

### 1. Prepare the Web Servers
1. Install Nginx:

    sudo pacman install nginx -y

2. Create necessary directories:

   sudo mkdir -p /var/lib/webgen/bin /var/lib/webgen/documents

3. Set permissions:
   sudo chown -R webgen:http /var/lib/webgen
   sudo chmod 755 /var/lib/webgen

### 2. Deploy the Files

1. Copy generate_index to /var/lib/webgen/bin/:

    cp generate_index /var/lib/webgen/bin/
    sudo chmod +x /var/lib/webgen/bin/generate_index

2. Copy index.html to /var/lib/webgen/:

    cp index.html /var/lib/webgen/

3. Configure Nginx:
    
    Copy server-block.conf to /etc/nginx/sites-available/:
    cp server-block.conf /etc/nginx/sites-available/

4. Creae a Systemlink: 

    sudo ln -s /etc/nginx/sites-available/server-block.conf /etc/nginx/sites-enabled/

5. Restart Nginx: 

    sudo systemctl reload nginx

### 3. Test the Servers

1. Verify the main page:

    curl http://<server-ip>/
2.Verify the /documents/ directory:
    
    curl http://<server-ip>/documents/

### 4. Configure the Load Balancer

1. Log in to DigitalOcean.
2. Create a load balancer in the same region as the servers.
3. Add both servers to the backend pool.
4. Test the load balancer's IP address in your browser:
Ensure it alternates traffic between servers.



