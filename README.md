# 2420 Assignment 3

## Overview
This project configures an Arch Linux server to display system information on a web page using:
- A script (`generate_index`) that generates an `index.html` file with system details.
- A systemd service and timer to automate the HTML generation.
- Nginx as the web server to serve the HTML file.

## Files in This Repository
1. **`generate_index`**: The script that generates the `index.html` file.
2. **`generate-index.service`**: A systemd service to run the script.
3. **`generate-index.timer`**: A systemd timer to schedule the service.
4. **`nginx.conf`**: The main Nginx configuration file.
5. **`server-block`**: The server block configuration for Nginx.
6. **`screenshots/`**: Contains a screenshot of the final success page.
7. **`README.md`**: This file, explaining the setup process.

---

## How to Set Up

### Step 1: Install Dependencies
Ensure that Nginx and systemd are installed on your server. If not, install them:
bash
sudo pacman -S nginx

## Step 2: Place Files in the Correct Locations

### 2.1 Copy the Script
Place the `generate_index` script in `/var/lib/webgen/bin/` and set executable permissions:

sudo mkdir -p /var/lib/webgen/bin
sudo cp generate_index /var/lib/webgen/bin/
sudo chmod +x /var/lib/webgen/bin/generate_index


## 2.2 Copy the Systemd Files
Place the service and timer files in /etc/systemd/system/:


sudo cp generate-index.service /etc/systemd/system/
sudo cp generate-index.timer /etc/systemd/system/
## 2.3 Reload systemd and Enable the Timer
Reload systemd, enable the timer, and start it:


sudo systemctl daemon-reload
sudo systemctl enable generate-index.timer
sudo systemctl start generate-index.timer

### Step 3: Configure Nginx
3.1 Copy the Server Block File
Place the server-block file in /etc/nginx/sites-available/:
sudo cp server-block /etc/nginx/sites-available/webgen

## 3.2 Enable the Server Block
Create a symbolic link to enable the server block:

sudo ln -s /etc/nginx/sites-available/webgen /etc/nginx/sites-enabled/webgen

### 3.3 Update the Nginx Configuration
Ensure your nginx.conf includes the following line in the http block:

nginx
include /etc/nginx/sites-enabled/*;

### 3.4 Restart Nginx
Test and restart Nginx to apply changes:

sudo nginx -t
sudo systemctl restart nginx

### Step 4: Verify the Setup
Open your browser and visit:
arduino
http://143.198.227.232
You should see a page displaying the following system information:
Kernel Release
Operating System
Date
Number of Installed Packages
### Step 5: Additional Notes
If you make changes to the script or server configuration, restart the necessary services:

sudo systemctl restart generate-index.service
sudo systemctl restart nginx
Ensure the /var/lib/webgen/HTML directory is writable by the webgen user:
sudo chown -R webgen:webgen /var/lib/webgen
sudo chmod -R 755 /var/lib/webgen
Deliverables
GitHub Repository
Link to Repository
IP Address
http://143.198.227.232
Screenshot
The final success screenshot is located in the screenshots folder as success.png.
### Step 6: How to Add This README to Your Repository
Open README.md in nvim:

nvim README.md
Paste the above content.

Save and exit:

:wq
Commit and push the changes:

git add README.md
git commit -m "Updated README with detailed steps"
git push origin main

