curl -fsSL https://get.docker.com -o install-docker.sh
sudo sh install-docker.sh

挂载卷
sudo docker run -d -p 80:80 -v /home/ricardo/nginx/html/sky:/usr/share/nginx/html nginx                                             
================================ ==========                                           
   Docker 基本命令                                                                       
   ================================ ==========                                           
                                                                                         
   ## 镜像操作                                                                           
   docker pull 镜像名        # 拉取镜像                                                  
   docker images            # 查看本地镜像                                               
   docker rmi 镜像名         # 删除镜像                                                  
   docker build -t 名字 .    # 从 Dockerfile 构建镜像                                    
                                                                                         
   ## 容器操作                                                                           
   docker ps                # 查看运行中的容器                                           
   docker ps -a             # 查看所有容器（含停止的）                                   
   docker run 镜像名        # 创建并运行容器                                             
   docker run -d            # 后台运行                                                   
   docker run --name 名字    # 给容器起名字                                              
   docker run -p 宿主机端口:容器端口  # 端口映射                                         
   docker run -v 宿主机路径:容器路径  # 目录挂载                                         
   docker run -e 变量=值     # 传入环境变量                                              
                                                                                         
   docker stop 容器名/ID    # 停止容器                                                   
   docker start 容器名/ID    # 启动已停止的容器                                          
   docker restart 容器名/ID  # 重启容器                                                  
   docker rm 容器名/ID       # 删除容器                                                  
   docker rm -f 容器名/ID    # 强制删除（运行中也能删）                                  
                                                                                         
   docker exec -it 容器名 bash   # 进入容器内部                                          
   docker logs -f 容器名         # 查看容器日志（实时）                                  
   docker logs 容器名            # 查看日志                                              
                                                                                         
   ## 清理                                                                               
   docker system prune       # 清理无用的镜像、容器、网络                                
   docker system df          # 查看磁盘占用 


查看容器挂载到宿主机的目录
sudo docker volume inspect nginx_html

运行：run
后台：-d 
端口：-p 100（宿主机）：80 
挂载卷： -v /home/ricardo/nginx/html/sky:/usr/share/nginx/html 
容器命名： --name my_nginx2
容器类型：nginx
sudo docker run -d -p 100:80 -v /home/ricardo/nginx/html/sky:/usr/share/nginx/html --name my_nginx2 nginx


sudo docker run -d -p 100:80  -v /home/ricardo/nginx/html/sky:/usr/share/nginx/html -v /home/ricardo/nginx/conf/nginx.conf:/etc/nginx/conf.d/default.conf:ro --name my_nginx2 nginx