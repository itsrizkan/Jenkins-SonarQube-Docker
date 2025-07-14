# Jenkins-SonarQube-Docker

1. Launch 3 EC2 instances  
   - Jenkins  
   - SonarQube  
   - Docker  

2. Setup Jenkins Server  
   - Expose port 8080  
   - Install Java JDK  
   - Install Jenkins  
   - Install plugins  
     - Default plugins  
     - SonarQube Scanner  
     - SSH2 Easy  
   - Create a freestyle project  
     - Configure source code management - Git repo URL  
     - GitHub hook trigger for GITScm polling  

3. Create a webhook in GitHub to allow pull & push with Jenkins and test the connectivity  

4. Setup SonarQube Server  
   - Expose port 9000  
   - Install JDK 17  
   - Install SonarQube using `wget`, `unzip`, and `./sonar.sh`  
   - Create a manual project with Jenkins & GitHub  
   - Create a token for Jenkins  

5. Setup SonarQube on Jenkins  
   - Install SonarQube from Maven Central (Manage Jenkins > Global Tool Configuration)  
   - Configure SonarQube (Manage Jenkins > Configure System)  
   - Configure build step to execute SonarQube Scanner (add key)  
   - Add token  

6. Setup Docker Server  
   - Install Docker  
   - Add current user to Docker group  
     ```bash
     sudo usermod -aG docker ubuntu
     newgrp docker
     ```

7. Give access to `jenkins` user@Jenkins server to SSH into Docker server  
   - On Docker server, edit sshd config file to enable public key authentication  
   - On Jenkins server, generate public and private keys and copy to Docker server  

8. Add Docker server to Jenkins to execute (Manage Jenkins > Configure System)  
   - Add a server group list  
   - Add the Docker server  
   - Edit build step to execute remote shell on build step for testing  
     ```bash
     touch test.txt  # remove later
     ```

9. Create a Dockerfile  

10. Edit build step to execute local shell (post-build actions)  
    ```bash
    scp -r ./* ubuntu@docker-server-ip:~/website/
    ```

11. Edit build step to execute remote shell (post-build actions)  
    ```bash
    cd /home/ubuntu/website
    docker build -t mywebsite .
    docker run -d -p 8085:80 --name=My-Website mywebsite
    ```

12. Expose port 8085 on Docker server


