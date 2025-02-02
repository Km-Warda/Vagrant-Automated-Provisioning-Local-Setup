# Automation for a local setup using Vagrant for 
Vagrant starts the reuired VMs on the required hypervisor, and uses shell scripts "`vagrant/*.sh` files" for configuring each service
```
vagrant up
``` 
# Workflow
![image](https://github.com/user-attachments/assets/099fc630-adbd-4315-a014-38c1a6bfa572)
### Nginx as a load balancer
Entry point to the users & forwarding the request to the application server
- hostname used for the Nginx VM is web01:
    - When a client accesses `web01`, the NGINX server on `web01` forwards the request to the backend servers.
### Apache TOMCAT Server
The server for the Java application
- the backend server hostname used is `app01`, configured in nginx setup script & `Vagranfile`
### RabbitMQ
Traffic forwarded from the web server to the message broker, sending a request to MemCache
### MemCache
For database caching
### MySQL Server
The main database

# Testing The Setup
1) Access `http://web01`
2) You should be forwarded to `http://web01/login`, thus TOMCAT server is running.
3) login with the test user
```
username: admin_vp
Password: admin_vp
```
4) Check RabbitMQ Responce from the button `RabbitMQ`
5) Check DB availability from the button `All Users`
6) Click on a user & the data will be fetched from the DB,
![image](https://github.com/user-attachments/assets/98fde5f3-1645-487b-8eee-324d31323d9f)
7) Exit & check the same user, the responce should be from the MemCache
![image](https://github.com/user-attachments/assets/55bbe63b-1c2a-4d24-96bb-de8e2b12627e)
