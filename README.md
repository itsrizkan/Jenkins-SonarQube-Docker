# Jenkins-SonarQube-Docker
1.Launch 3 EC2 instances 
    Jenkins
    SonarQube
    Docker
2.Setup Jenkins Server
    expose port 8080
    install java jdk
    install jenkins
    install plugins
        default plugins
        SonarQube Scanner
        SSH2 Easy
    create a freestyle project
        configure source code management - git repo url
        github hook trigger for GITScm polling
3.Create a webhook in github to allow pull & push with jenkins && test the connectivity
4.Setup SonarQube Server
    expose port 9000
    install jdk 17
    install sonarqube using wget && unzip && ./sonar.sh
    create a manual project with jenkins & github
    create a tocken for jenkins
5.Setup sonarqube on jenkins
    install sonarqube from maven central; automatically (manage jenkins>global tool config)
    configure sonarqube (manage jenkins>config system)
    configure build step to execute sonaqube scanner (add key)
    add tocken
6.Setup docker server
    intall docker
    add current user to docker group 
        $sudo usermod -aG docker ubuntu
        $newgrp docker
7.Give access to jenkins user@jenkins server to ssh docker server
    on docker server, edit sshd file to enable public authentication 
    on jenkins server, genrate public and private && copy to docker server
8.Add docker server to jenkins to execute (manage jenkins>config system)
    add a server group list
    add the docker server
    Edit build step to execute remote shell on build step for testing $touch test.txt (post build actions) #remove later
9.Create a Dockerfile
10.Edit build step to execute local shell (post build actions)
    $scp -r ./* ubuntu@docker-server-ip:~/website/ #copy local file to docker server
11.Edit build step to execute remote shell (post build actions)
    $cd /home/ubuntu/website
    $docker build-t mywebsite .
    $docker run -d -p 8085:80 --name=My-Website mywebsite
12.Expose port 8085 on docker server



