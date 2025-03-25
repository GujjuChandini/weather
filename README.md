# weather

sudo yum install nginx -y   # For Amazon Linux
sudo apt install nginx -y   # For Ubuntu


sudo systemctl start nginx
sudo systemctl enable nginx


sudo cp -r $WORKSPACE/index.html /usr/share/nginx/html/
sudo cp -r $WORKSPACE/style.css /usr/share/nginx/html/
sudo cp -r $WORKSPACE/images /usr/share/nginx/html/
sudo systemctl restart nginx


http://<EC2-Public-IP>/index.html
