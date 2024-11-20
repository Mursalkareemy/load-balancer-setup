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
```bash
sudo pacman -S nginx

