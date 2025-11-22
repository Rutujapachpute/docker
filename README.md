
☁️ Steps for AWS EC2 Setup
Create EC2 Instance

Chose Ubuntu 22.04 (free tier t2.micro).

Created key pair (.pem file) to connect.

In Security Group, opened ports:

22 (SSH) → so I can connect
8080 (TCP) → so I can see my website
Connect to EC2 (from my computer terminal):

ssh -i mykey.pem ubuntu@<EC2-Public-IP>
Update EC2 and Install Docker:

sudo apt update
sudo apt install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ubuntu
👣 Steps I took for Docker Project (like a recipe)
Make a folder for my project

mkdir mydockerapp
cd mydockerapp
Create a simple web page

echo "<h1>Hello, Docker</h1>" > index.html
Create a Dockerfile

vim Dockerfile
FROM httpd:2.4
COPY index.html /usr/local/apache2/htdocs/
:wq! ((save the file)
👉 This means:

“Hey Docker, use Apache as base”
“Copy my index.html inside Apache’s web folder”
Build my Docker image

sudo docker build -t my-apache-server .
Run my container

sudo docker run -p 8080:80 -d my-apache-server
👉 This means:

Port 80 inside container → Port 8080 on EC2
Run in background mode
Check it’s running

sudo docker ps
Open in browser

http://<EC2-Public-IP>:8080
🎉 I saw my page: Hello, Docker!
