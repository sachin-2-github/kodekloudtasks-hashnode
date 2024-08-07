---
title: "Task- Setup SSL for Nginx"
seoTitle: "Task- Setup SSL for Nginx"
seoDescription: "Task- Setup SSL for Nginx"
datePublished: Fri Jun 30 2023 09:07:34 GMT+0000 (Coordinated Universal Time)
cuid: cljicpnp200080amign3z8c8r
slug: task-setup-ssl-for-nginx
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1688402273243/69198b91-acda-4797-a599-cf1733f3b77f.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1688116013359/6deeb73d-9fb2-4cbd-98f4-e51d09116e72.png
tags: linux, kodekloud

---

## Problem:

> The system admins team of `xFusionCorp Industries` needs to deploy a new application on `App Server 3` in `Stratos Datacenter`. They have some pre-requites to get ready that server for application deployment. Prepare the server as per requirements shared below:
> 
> 1. Install and configure `nginx` on `App Server 3`.
>     
> 2. On `App Server 3` there is a self signed SSL certificate and key present at location `/tmp/nautilus.crt` and `/tmp/nautilus.key`. Move them to some appropriate location and deploy the same in Nginx.
>     
> 3. Create an `index.html` file with content `Welcome!` under Nginx document root.
>     
> 4. For final testing try to access the `App Server 3` link (either hostname or IP) from `jump host` using curl command. For example `curl -Ik https://<app-server-ip>/`.
>     

## Solution:

*<mark>Please ensure to review the task instructions carefully and modify the commands according to your specific server, username, and other relevant details.</mark>*

1. ssh into the App server3 with the sudo privileges
    
2. Install the `EPEL` repo for the `Nginx` package
    
    ```plaintext
     sudo yum install epel-release -y
    ```
    
3. Install `Nginx`
    
    ```plaintext
    sudo yum install nginx -y
    ```
    
4. Check version
    
    ```plaintext
    nginx -v
    ```
    
5. Start the `Nginx` service and check the status.
    
    ```plaintext
    sudo systemctl start nginx && systemctl status nginx
    ```
    
    > *Now we have installed the Nginx properly*
    > 
    > Let's do some configurations
    > 
    > * Create `index.html` file under the `nginx` root directory
    >     
    > * To see the Root directory of the `nginx` Navigate to `/usr/share/nginx/html` directory
    >     
    > * Now do `ls -al index.html`
    >     
    > 
    > *Note: You will find a link*`index.html`*pointing to the original file. Go to that pointed file and edit that*`index.html`*file. If it exists there o/w create a new file under that directory. So in our case, the*`HTML`*directory was created under the '*`doc/`*' directory. So I had to create it and edit the index.html file*
    > 
    > ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688212028930/8fc5120d-7544-4542-9f61-dfc4cf52eacd.png align="center")
    > 
    > The steps I did were
    > 
    > * Created HTML directory stepping back to 2 steps under `doc` directory.
    >     
    > * Created index.html file under it ( i.e HTML/index.html)
    >     
    > * Added HTML content `Welcome!` Inside `index.html`
    >     
    
6. Copy or move the `nautilus.crt` and `nautilus.key` under `/etc/nginx/` or any other directory you would prefer
    
7. Edit the config file located at `/etc/ngix/nginx.conf` Uncomment the entire server block and mention the `certificate` and `key` file path like below.
    
    ```plaintext
    ssl_certificate     /etc/nginx/nautilus.crt;
    ssl_certificate_key  /etc/nginx/nautilus.key;
    ```
    
8. Restart the Nginx server.
    
    ```plaintext
    sudo systemctl restart nginx
    ```
    
9. Access the site with the curl command
    
    ```plaintext
    curl -Ik https://<Ip/hostname of app-server3>
    ```
    

Response should be `200 ok.`

### Know me:

Hi, I am Sachin Khamitkar, a passionate devops engineer and an Expert Support Engineer. As a DevOps enthusiast and technology fan, I am passionate about automating workflows, optimizing infrastructure, and improving deployment processes. I love sharing insights on cloud strategies, containerization, and continuous delivery. With 6 years of experience in Technical and Application Support, I have a strong foundation in DevOps practices. I excel in root cause analysis, SLA adherence, and enhancing software stability. My skills include log analysis, SQL reporting, and CI/CD pipeline optimization. I have a proven track record in deploying builds, patches, and maintaining production environments. Additionally, I bring expertise in incident, problem, and change management following ITIL standards. If you're as excited about DevOps as I am, let's connect 🌟 me on [LinkedIn](https://www.linkedin.com/in/sachin-khamitkar)🔗💼, [GitHub](https://github.com/sachin-2-github)💻🔗, and [Email](mailto:sachin.bmp@gmail.com)📧 for more tech tips, tutorials, and exciting projects! Let's innovate together and drive the future of DevOps! 🚀👩‍💻💡