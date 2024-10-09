# Spring Boot based Shopping Cart Web App Deployment _ End-End CI/CD Project

![image](https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment/assets/86109995/50483368-44d8-4409-af22-9e1be711c8e0)


Create 3 EC2 Instances with 20GB storage, 4GB RAM and choose t2.medium

![image](https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment/assets/86109995/d67e8e6a-6bde-4013-afd2-3973457947b6)

When you create the instances, please create a security group to allow inbound and outbound traffic.

![image](https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment/assets/86109995/df26d93a-0c09-4552-b27a-8cbf286085a8)

Here, MobaXtreme is used to ssh into and configure each EC2 instance

![image](https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment/assets/86109995/0607acc5-aabf-4845-a991-c41b08cf40df)

### Install Docker on All 3 VMs
### trying something step to step
#### Step-by-Step Installation

#### 1. Install prerequisite packages: 
   
```bash
   sudo apt-get update 
   sudo apt-get install ca-certificates curl
```

#### 2. Download and add Docker's official GPG key:

```bash
   sudo install -m 0755 -d /etc/apt/keyrings 
   sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc 
   sudo chmod a+r /etc/apt/keyrings/docker.asc
```

#### 3. Add Docker repository to Apt sources:

```bash
   echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
      $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

   sudo apt-get update
```

#### 4. Update package index:
  
```bash 
   sudo apt-get update
```

#### 5. Install Docker packages:
   
```bash
   sudo apt-get install docker-ce docker-ce-cli containerd.io -y
```

#### 6. Grant permission to Docker socket (optional, for convenience):

```bash
   sudo chmod 666 /var/run/docker.sock
```

Following these steps, you should have successfully installed Docker on your Ubuntu system. You can now start using Docker to containerize and manage your applications.

Follow this official document if you find any errors: Link: https://docs.docker.com/engine/install/ubuntu/

### Setting Up Jenkins on Ubuntu

#### Step-by-Step Installation

#### 1. Update the system:

```bash
   sudo apt-get update
   sudo apt-get upgrade -y
```

#### 2. Install Java (Jenkins requires Java):

```bash
   sudo apt install -y fontconfig openjdk-17-jre-headless -y
```

#### 3. Add Jenkins repository key:

```bash
   sudo wget -O /usr/share/keyrings/Jenkins-keyring.asc \
   https://pkg.Jenkins.io/debian-stable/Jenkins.io-2023.key
```

#### 4. Add Jenkins repository:

```bash
   echo \
      "deb [signed-by=/usr/share/keyrings/Jenkins-keyring.asc] \
      https://pkg.Jenkins.io/debian-stable binary/" | \
      sudo tee /etc/apt/sources.list.d/Jenkins.list > /dev/null
```

#### 5. Update the package index:

```bash
   sudo apt-get update
```

#### 6. Install Jenkins:

```bash
   sudo apt-get install -y Jenkins
```

#### 7. Start and enable Jenkins:

```bash
   sudo systemctl start Jenkins
   sudo systemctl enable Jenkins
```

#### 8. Access Jenkins:

   - Open a web browser and go to http://your_server_ip_or_domain:8080.
   - You will see a page asking for the initial admin password. Retrieve it using: sudo cat /var/lib/Jenkins/secrets/initialAdminPassword
   - Enter the password, install suggested plugins, and create your firstadmin user. or follow this official document link: https://www.Jenkins.io/doc/book/installing/linux/#debianubuntu



### Clone the repository, create your repository, and push those into your GitHub repository

#### 1. Clone the repo:

```bash
git clone https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment.git

```

#### 2. Initialize Git Repository

```bash
git init
```

#### 3. Add Files to Git:

```bash
# Stage all files for the first commit:

git add .
```

#### 4. Commit Files:

```bash
# Commit the staged files with a commit message:

git commit -m "Initial commit"
```

#### 5. Change the remote repo

```
git remote add new-origin https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment.git
```
replace with your GitHub repo

#### 6. Push to GitHub:

```bash
# Push the local repository to GitHub:

git push -u origin main
```


### SonarQube Setup:

-ssh into sonarqube ec2 instance

-run -> docker run -d –name sonar -p 9000:9000 sonarqube:lts-comminity

-access using <public_ip:9000>

username: admin
password:admin

### Nexus Setup:

-ssh into nexus ec2 instance

-run -> docker run -d –name nexus -p 8081:8081 sonatype/nexus3 

-access using <public_ip:8081>

-go inside of the sonatype/nexus3 container: docker exec -it <container_id> /bin/bash 

-sign to nexus using the username: admin and password; the password is stored in ‘sonatype-work/nexus3/admin.password’. 
 
-view it using cat sonatype-work/nexus3/admin.password' command.


### Installing Trivy on Jenkins Server

Step-by-Step Installation

#### 1. Install prerequisite packages:

```bash
sudo apt-get install wget apt-transport-https gnupg lsb-release
```

#### 2. Add Trivy repository key:

```bash
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null | sudo apt-key add -
```
#### 3. Add Trivy repository to sources:

```bash
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
```
#### 4. Update package index:

```bash
sudo apt-get update
```

#### 5. Install Trivy:

```bash
sudo apt-get install trivy -y
```

or follow this official document link: https://aquasecurity.github.io/trivy/v0.18.3/installation/


===========================================================================================================

### Install Plugins in Jenkins

1. Eclipse Temurin installer -> for jdk
2. Sonarqube scanner
3. Docker
4. Docker pipeline
5. ClodBees Docker Build and Publish
6. docker-build-step
7. OWASP Dependency-Check
8. Config file provider -> for Nexus
9. Nexus Artifact Uploader
10. Kubernetes
11. Kubernetes cli
12. Kubernetes credentials
13. Kubernetes clint api
14. Maven integration
15. Pipeline Maven integration Plugin

Now we installed the tools and Now we need to configure them

Go to manage Jenkins -> Tools

1. Jdk -> name= jdk17 , install automatically from adoptium.net, version= jdk17 latest
2. Sonarqube scanner -> name= sonar-scanner, Install automatically
3. Maven -> name= maven3, version= 3.6.3
4. Dependency-Check installation -> name= dependency-check, version= dependency-check6.5.1
5. Docker -> name=docker, install automatically from docker.com


### Configure the SonarQube server in Jenkins

1. Firstly generate the token in SonarQube
   
Goto Administration -> security -> users -> update token -> name= sonar-token and
generate

![sonar1](https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment/assets/86109995/9fea03b6-ea35-4067-a0b8-1684850c3b9a)


2. Add the token to Jenkins

Goto manage Jenkins -> credentials -> global -> kind= secret text -> secret=<your-token>, id=sonar-token, description=sonar-token

![sonar2](https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment/assets/86109995/6f797a03-29bf-4ed2-94b0-32e8382d6ee3)

3. Configure SonarQube servers in Jekins

Go to manage Jenkins -> system -> sonarqube server -> name=sonar, url=http://<public_ip>:9000, token=sonar-token

![sonar3](https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment/assets/86109995/94d07ab4-392b-495d-881c-782ab9f1474a)


### Configure the Nexus server in Jenkins


Nexus authentication with Jenkins:

Go to manage Jenkins -> manage files -> add new config -> select Global Maven settings.xml,
id=maven-setting & click next

Go to content and add; 

i) servers with the id = maven-releases, username, and password of the Nexus instance. (one we are going to release for production environments) \
ii) servers with the id = maven-snapshots, username, and password of the Nexus instance. (one we are going to release for development environments)

![555555](https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment/assets/86109995/f9e804dd-a126-4052-889a-e93116a7c32d)


Nexus Configuration:

Update your pom.xml file with your Nexus repositories.

Copy the maven-releases URL, and maven-snapshots URL from the Nexus Repository  and update in the pom.xml file in the code repository.

![Screenshot from 2024-07-07 03-02-58](https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment/assets/86109995/b2ac7bd5-717e-47de-b459-273a1df0da6e)



### Create the pipeline in Jenkins.

Now write the Jenkinsfile

```
pipeline {
   agent any
   
   tools {
      jdk 'jdk17'
      maven 'maven3'
   }
   
environment {
   SCANNER_HOME = tool 'sonar-scanner'
}

stages {
   stage('Git Checkout') {
      steps {
         git branch: 'main', url: ‘https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment.git’
            }
}

   stage('Compile') {
      steps {
         sh "mvn compile"
      }
   }
   
   stage('Unit Test') {
      steps {
         sh "mvn test -DskipTests=true"
      }
   }
   
   stage('SonarQube Analysis') {
      steps {
         withSonarQubeEnv('sonar') {
            sh '''$SCANNER_HOME/bin/sonar-scanner 
            -Dsonar.projectKey=Ekart 
            -Dsonar.projectName=Ekart 
            -Dsonar.java.binaries=.'''
         }
      }
   }

   stage('OWASP Dependency Check') {
      steps {
         dependencyCheck additionalarguments: ' --scan ./', odcInstallation: 'dependency-check' 
         dependencyCheckPublisher pattern: '**/dependency-check-report.xml' 
         }
      }
   }

   stage('Build') {
      steps {
         sh "mvn package -DskipTests=true"
      }
   }

   stage('Deploy Artifacts To Nexus') {
      steps {
         withMaven(globalMavenSettingsConfig: 'maven-setting', jdk: 'jdk17', maven: 'maven3', mavenSettingsConfig: '', traceability: true) {
            sh "mvn deploy -DskipTests=true"
         }
      }
   }

   stage('Build & Tag Docker Image') {
      steps {
         script {
            withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
               sh "docker build -t ravdas/ekart:latest -f docker/Dockerfile ."
            }
         }
      }
   }

   stage('Trivy Scan Image') {
      steps {
         sh "trivy image ravdas/ekart:latest > trivy-image-report.txt"
      }
   }

   stage('Publish Docker Image') {
      steps {
            script {
               withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                  sh "docker push ravdas/ekart:latest"
               }
            }
      }
   }

   stage('Deploy to Kubernetes') {
      steps {
         withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://172.31.8.162:6443')
         # for the serveUrl: use the <ip_address_master:inbound port declared for K8S Cluster>
         {
            sh "kubectl apply -f deploymentservice.yml -n webapps"
            sh "kubectl get svc -n webapp"
         }
      }
   }

```


### Setup K8 Cluster

Create one master and two worker nodes (3 EC2 instances with 20GB storage, t2.medium, Ubuntu image)

![Screenshot from 2024-07-07 00-47-34](https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment/assets/86109995/b0ed4b7c-a0fc-43bc-b831-00627e56fd77)


#### 1. Update System Packages [On Master & Worker Nodes]

```bash
sudo apt-get update
```

#### 2. Install Docker[On Master & Worker Nodes]

```bash
sudo apt install docker.io -y
sudo chmod 666 /var/run/docker.sock
```

#### 3. Install Required Dependencies for Kubernetes[On Master & Worker Nodes]

```bash
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
sudo mkdir -p -m 755 /etc/apt/keyrings
```

#### 4. Add Kubernetes Repository and GPG Key[On Master & Worker Nodes]

```bash
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

#### 5. Update Package List[On Master & Worker Node]

```bash
sudo apt update
```

#### 6. Install Kubernetes Components[On Master & Worker Nodes]

```bash
sudo apt install -y kubeadm=1.28.1-1.1 kubelet=1.28.1-1.1 kubectl=1.28.1-1.1
```

#### 7. Initialize Kubernetes Master Node [On MasterNode]

```bash
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

After running the above command, you will receive the below-highlighted. Run that on the worker nodes to join them with the master node.

![image](https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment/assets/86109995/8db6b226-294f-4790-bf93-2ecc9fae3bec)

#### 8. Configure Kubernetes Cluster [On MasterNode]

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

#### 9. Deploy Networking Solution (Calico) [On MasterNode]

```bash
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

#### 10. Deploy Ingress Controller (NGINX) [On MasterNode]

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.49.0/deploy/static/provider/baremetal/deploy.yaml
```



### Create a Service Account, Role & Assign that role, create a secret for the Service Account, and generate a Token in the Jenkins server


First create the namespace using,

```bash
kubectl create namespace webapps
```

#### Creating Service Account

Create a yaml file(sa.yml) with the following;

```bash
   apiVersion: v1
   kind: ServiceAccount
   metadata:
      name: jenkins
      namespace: webapps
```
execute the yaml file

```bash
kubectl apply -f sa.yml
```

#### Creating a Role

Create a yaml file(role.yml) with the following;

```bash
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
   name: app-role
   namespace: webapps
rules:
   - apiGroups:
   - ""
   - apps
   - autoscaling
   - batch
   - extensions
   - policy
   - rbac.authorization.k8s.io
resources:
   - pods
   - secrets
   - componentstatuses
   - configmaps
   - daemonsets
   - deployments
   - events
   - endpoints
   - horizontalpodautoscalers
   - ingress
   - jobs
   - limitranges
   - namespaces
   - nodes
   - pods
   - persistentvolumes
   - persistentvolumeclaims
   - resourcequotas
   - replicasets
   - replicationcontrollers
   - serviceaccounts
- services
   verbs: ["get", "list", "watch", "create", "update", "patch", "delete"]

```
execute the yaml file

```bash
kubectl apply -f role.yml
```

#### Bind the role to service account

Create a yaml file(assign.yml) with the following;

```bash

apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
   name: app-rolebinding
   namespace: webapps
roleRef:
   apiGroup: rbac.authorization.k8s.io
   kind: Role
   name: app-role
subjects:
-  namespace: webapps
   kind: ServiceAccount
   name: jenkins
```
execute the yaml file

```bash
kubectl apply -f assign.yml
```

#### Generate token using service account in the namespace

Create a yaml file(sec.yml) with the following;

```bash
'''
apiVersion: v1
kind: Secret
type: kubernetes.io/service-account-token
metadata:
   name: mysecretname
   annotations:
   kubernetes.io/service-account.name: myserviceaccount

```

execute the yaml file

```bash
kubectl apply -f sec.yml -n webapps
```
To view the secret token,

```bash
kubectl -n webapps describe secret mysecretname
```

Add this token to the Jenkins server

Goto manage Jenkins -> credentials -> global -> kind= secret text, secret= <token>, id= k8-token

![5565656](https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment/assets/86109995/0851a961-6106-4751-a4ce-a2f5de60c1f0)


### Final Results

1. Jenkin Pipeline build is a Success
   
![image](https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment/assets/86109995/d758f259-1a77-4fe6-b3be-4d27a466b08a)

Access the application with the <work node 1 or 2 IP address of K8S Cluster:port received after the build (Highlighted in the above image)>

2. Deployment of the Application
   
![Screenshot from 2024-07-07 03-04-22](https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment/assets/86109995/8eabb6b6-6a84-46af-8210-7a1d64e4d442)

![Screenshot from 2024-07-07 03-04-19](https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment/assets/86109995/98d2475a-182b-4a89-9d0d-980d5a35a7a0)

3. SonarQube Code Analysis
   
![Screenshot from 2024-07-07 03-03-48](https://github.com/RavDas/Spring-Boot-Shopping-Cart-Web-App-Deployment/assets/86109995/3588833e-c510-4d1b-baf4-17b08c940036)






<!--Testing for CI Integration again-->