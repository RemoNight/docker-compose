# Steps to use docker-compose for install services: GitLab & Jenkins

### Uninstall old versions & Install using the repository
1. Uninstall docker (If you have older versions of docker) on your machine.
```
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```
2. Update the apt package and install packages to allow apt to use a repository.
```
$ sudo apt-get update
$ sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
3. Add Docker’s official GPG key.
```
$ sudo mkdir -p /etc/apt/keyrings
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
4. Use this command to set up the repository.
```
$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Install the latest version of docker
1. Update the apt package & install Docker Engine, Containerd, Docker Compose.
```
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```
2. List the version of docker to select a specific version.
```
$ apt-cache madison docker-ce
```
3. Select & Install a specific version of docker. (Example select version: 5:20.10.17~3-0~ubuntu-focal)
```
$ sudo apt-get install docker-ce=5:20.10.17~3-0~ubuntu-focal docker-ce-cli=5:20.10.17~3-0~ubuntu-focal containerd.io docker-compose-plugin
```
4. Verify that Docker Engine is installed correctly by running the hello-world image.
```
$ sudo docker run hello-world
```

### Docker-compose
1. Use this command to verify that Docker Compose is available.
```
$ docker-compose -v
```
2. Create directory to store docker-compose.yml file.
```
$ mkdir test-docker-compose
$ mkdir ~/jenkins_home 
$ export GITLAB_HOME=$(pwd)/gitlab
$ cd test-docker-compose
```
3. Download docker-compose.yml file and store this file in directory: test-docker-compose

4. Use this command to start the container.
```
$ docker-compose up -d
```
5. Completed

### Jenkins
- set port of jenkins is 8080:8080
1. Go to the browser http://localhost:8080 (Example: http://27.254.99.183:8080)
![image](uploads/849a09b90242c7f436885051c229b071/image.png)
2. After running the Docker command successfully. Use this command to get a first password for login jenkins
```
$ docker exec jenkins-lts cat /var/jenkins_home/secrets/initialAdminPassword
```
3. Completed. you can install Jenkins on docker container successfully.

### GitLab
- set port of gitlab is 8081:80
1. Go to the browser http://localhost:8081 (Example: http://27.254.99.183:8081)
![image](uploads/33cc16203207d3815c8892eba63fdb1c/image.png)
2. Default username: root & use this command to get a first password for login gitlab (After running the Docker command successfully)
```
$ docker exec -it gitlab-ce grep 'Password:' /etc/gitlab/initial_root_password
```
3. Completed. you can install GitLab on docker container successfully.
