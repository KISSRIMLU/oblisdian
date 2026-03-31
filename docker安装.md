curl -fsSL https://get.docker.com -o install-docker.sh
sudo sh install-docker.sh

挂载卷
sudo docker run -d -p 80:80 -v /home/ricardo/nginx/html/sky:/usr/share/nginx/html nginx                                             