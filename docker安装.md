curl -fsSL https://get.docker.com -o install-docker.sh
sudo sh install-docker.sh

挂载卷
   sudo docker run -d --name nginx -p 80:80 -v /home/ricardo/nginx/html:/usr/share/nginx/html nginx                                             