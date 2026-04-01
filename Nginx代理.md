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

| 名称         | 说明                                 |
| ---------- | ---------------------------------- |
| 轮询         | 默认方式                               |
| weight     | 权重方式，默认为 1，权重越高，被分配的客户端请求就越多       |
| ip_hash    | 依据 ip 分配方式，这样每个访客可以固定访问一个后端服务      |
| least_conn | 依据最少连接方式，把请求优先分配给连接数少的后端服务         |
| url_hash   | 依据 url 分配方式，这样相同的 url 会被分配到同一个后端服务 |
| fair       | 依据响应时间方式，响应时间短的服务将会被优先分配           |
