# 反向代理：客户端发起请求到Nginx，Nginx转发到服务器。不对外暴露业务更安全。
## 1.
服务端请求地址：http://域名/api/employee/login
## 2.
Nginx代理：
```nginx
	server {
		#nginx监听服务器80或https(443)端口
        listen       80;  
        server_name  localhost; 
        
        #截取/api/重写
        location /api/{
            proxy_pass http://tomcat:8080/admin/;
        }
    }
```
## 3.
后端接收：http://tomcat:8080/admin/employee/login

---

# 负载均衡：底层反向，分散流量
## 1.
多个服务端发起请求到：http://域名/api/employee/login

## 2.
Nginx代理：
```nginx
	#分配服务器
	upstream ==webservers=={
		server tomcat1:8080 weight=90;
		server tomcat1:8080 weight=10;
	}

	server {
        listen       80;  
        server_name  localhost; 
        
        #负载均衡
        location /api/{
            proxy_pass http://==webservers==/admin/;
        }
    }
```
##  3.

策略：
