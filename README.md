# Static Website Deployment on AWS EC2 with NGINX

This project involves deploying a static website to an AWS EC2 instance using NGINX as the web server. The website showcases basic information including the name, username, and email address.

## Project Overview

- **Cloud Platform**: AWS EC2
- **Web Server**: NGINX
- **Static Website**: HTML, CSS, and JavaScript files containing the following details:
  - **Name**: Kudirat Zubair
  - **Username**: ameerah
  - **Email**: [kudirat**********@gmail.com](mailto:kudirat************@gmail.com)

## Prerequisites

1. **AWS Account**: Ensure you have an AWS account.
2. **EC2 Instance**: Launch an Ubuntu-based EC2 instance.
3. **SSH Key**: Configure SSH access to the EC2 instance using your private key.
4. **NGINX**: Install and configure NGINX on the EC2 instance.
5. **Static Website Files**: Have the static website files (HTML, CSS, JavaScript) ready for deployment.

## Deployment Steps

### 1. Launch EC2 Instance

- Log in to your AWS Management Console.
- Navigate to the EC2 dashboard and launch a new instance with the following:
  - **AMI**: Ubuntu Server 20.04 LTS (or later).
  - **Instance Type**: t2.micro (free tier eligible).
  - **Key Pair**: Select or create a key pair for SSH access.

### 2. Connect to the Instance

- Use your terminal or SSH client to connect to the instance:

  ```bash
  ssh -i your-key.pem ubuntu@<your-ec2-public-ip>
  ```

### 3. Install NGINX

- Update the package index and install NGINX:

  ```bash
  sudo apt update
  sudo apt install nginx -y
  ```

- Verify NGINX is running:

  ```bash
  sudo systemctl status nginx
  ```

### 4. Upload Static Website Files

- Use `scp` or another file transfer method to upload the static website files to the instance:

  ```bash
  scp -i your-key.pem index.html ubuntu@<your-ec2-public-ip>:/home/ubuntu
  ```

- Move the files to the NGINX default directory:

  ```bash
  sudo mv /home/ubuntu/index.html /var/www/html/
  ```

- (Optional) Upload additional files (CSS, JavaScript) and move them to `/var/www/html/`.

### 5. Configure NGINX

- Ensure the NGINX configuration serves the static content:

  ```bash
  sudo nano /etc/nginx/sites-available/default
  ```

  Replace the existing `location` block with:

  ```nginx
  location / {
      root /var/www/html;
      index index.html;
  }
  ```

- Restart NGINX to apply changes:

  ```bash
  sudo systemctl restart nginx
  ```

### 6. Access the Website

- Open your browser and navigate to `http://<your-ec2-public-ip>` to view the website.

## Project Structure

```plaintext
.
├── index.html
└── (Optional: Additional CSS/JS files)
```

## Notes

- Ensure the EC2 instance security group allows HTTP (port 80) traffic.
- Use a custom domain and SSL for a production-ready deployment.

## License

This project is licensed under the MIT License. Feel free to use and modify as needed.
