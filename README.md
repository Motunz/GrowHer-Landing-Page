# GrowHer- Empowering Women in the Digital Economy.

**Live Site**: [GrowHer Website](https://growher.duckdns.org/)

## 🚀 Features

- Dynamic User greetings with time based messages.
  
- Mission Statement and Personal Bio.
  
- Contact Form.
  
- Social Media Integration.
  
- Responsive Design.
  
- Hosted on AWS EC2.
  
- Used AWS S3 for Object Storage.
  
- Secured with SSL via Let's Encrypt (Certbot).
  
- Domain Management with DuckDNS.

## 🔧 Deployment Steps

1. **Setup a server using AWS EC2**

- Logged into my AWS account through the AWS console.
  
- Selected AWS EC2.
  
- Selected a region `eu-west-2` (London).
  
- Configured an instance:

  i. Name: Startup Prototype Server

  ii. AMI (OS): Ubuntu Server

  iii. Instance Type: t2.micro

  iv. Created and downloaded new key pair(prototype-key.pem)

  v. Network Settings: Allowed SSH(port 22), HTTP (port 40), and HTTPS (PORT 443) from anywhere.

- Launched Instance. 

2. **Connect to Server**

- Opened Local Terminal
  
- Navigated to the folder with my keypair. In my case its the Downloads folder.

```cd Downloads```

- Run:

```ssh -i "prototype-key.pem" ubuntu@ec2-13-40-229-156.eu-west-2.compute.amazonaws.com```

- Updated server:

```sudo apt update```

3. **Install Nginx**

- Run:

```sudo apt install nginx -y```

- Checked if nginx is running:

```sudo systemctl status nginx```

- Nginx is running. 

- Tested the nginx webserver with my EC2 public IP. It displayed the default Nginx page which confirm that my instance and nginx webserver are running fine. 

4. **Create Landing Page**

- Get into the default nginx dierectory to remove the default index.html file and create a new index.html file for my landing page:

```cd /var/www/html```

```sudo rm index.nginx-debian.html```

- Created my index.html file and added custom HTML code. 

```sudo nano index.html```

- Confirmed landing page renders via EC2 public IP .

<img width="1664" alt="Greeting Page Displayed on EC2 IP" src="https://github.com/user-attachments/assets/7928b59b-5cf8-4aff-a602-017037c8833a" />
  
<img width="1670" alt="Main Page Displayed on EC2 IP" src="https://github.com/user-attachments/assets/a6d84709-ac67-4f87-ae39-9962d67e7425" />



5. **Point Domain and Secure site with Let's Encrypt SSL (Certbot)**

- Setup a free domain on Duck DNS
  
- Linked Domain to EC2 IP

<img width="1395" alt="Domain Linked to IP" src="https://github.com/user-attachments/assets/447f95a4-1d80-4e70-b3cb-0996d0975ec0" />

[Landing Page rendered on Duck DNS domain](http://growher.duckdns.org)

- Installed Certbot on my EC2

```sudo apt update -y```

```sudo apt install -y epel-release```

```sudo apt install -y certbot python3-certbot-nginx```

- Added a server block file and added a new config to ensure my domain http://growher.duckdns.org serve the index.html from /var/www/html.

```sudo nano /etc/nginx/sites-available/growher```

- Enabled server block

```sudo ln -s /etc/nginx/sites-available/growher /etc/nginx/sites-enabled/```

- Tested and reloaded Nginx

```sudo nginx -t```

```sudo systemctl reload nginx```

- Install and configure SSL. Run Certbot: 

```sudo certbot --nginx -d growher.duckdns.org```

6. **Site Live and Secured**

<img width="1503" alt="Site Secured" src="https://github.com/user-attachments/assets/3021e1bc-c9cb-46c5-a251-2509ca9befc3" />

[GrowHer Website](https://growher.duckdns.org/)

