# nexus

Artifact Repository tool 
Nexus (officially Sonatype Nexus Repository Manager) is a repository manager used to store, manage, and distribute software artifacts used in application development and CI/CD pipelines.  
Artifacts -- By products when we build an application Ex: jar, war, pom  
nodejs -- .tgz   
python -- whl / wheel format  
dotnet -- nugget  

Need for artfacts ?  
you have a springboot application (v1) & you package it & get jar file as o/p. --> to run the appl. java -jar <jar file>   
you make some changes (v2) & u package & get a jar file as new o/p 
So, you have nexus to store different version of artifacts    
we have repos inside nexus for maven, . net, docker   

With Nexus ✅

  * Dependencies are cached
  * Builds are faster
  * Internet dependency is reduced
  * Central control & security
  * Versioned artifact storage

Three type of repos are there inside nexus 
  
    - proxy repos  :   used to cache repos from repote repos     
      Every time if the dependedncies are to be downloaded from maven central it takes lot of time , so they are downloaded first and then cached in nexus & from next time they are used from nexus   
      It proxies external repos like maven central, npmjs.org, dockerhub  
      download once then serves from cache   
    - Hosted: Custom artifacts (your)  
      can upload/ publish artifacts   
      acts as private artifact store   
      used for internal builds & releases   
      ex: Internal Maven libraries, Your Docker images, Company npm packages  
    - Grouped : can group proxy + hosted   
  

Repositories:  
| Format             | Used for                          |
| ------------------ | --------------------------------- |
| **Maven (maven2)** | Java, Spring, microservices       |
| **npm**            | Node.js packages                  |
| **Docker**         | Docker images                     |
| **NuGet**          | .NET packages                     |
| **PyPI**           | Python packages                   |
| **Yum**            | RPM-based Linux packages          |
| **APT**            | Debian/Ubuntu packages            |
| **Raw**            | Any generic files (zip, tar, exe) |
| **Helm**           | Kubernetes Helm charts            |
| **RubyGems**       | Ruby packages                     |

<img width="1536" height="1024" alt="ChatGPT Image Jan 20, 2026, 09_52_44 PM" src="https://github.com/user-attachments/assets/1480b92a-ab53-4cfb-bdfc-bfda62f0e102" />
We can also set clean up policies : Ex: if artifact >90 days artifact can be deleted  
Pre req: 4GB storage wherever you run nexus

Nexus Installation:

t2.medium ec2 instance 
```bash
sudo apt update  
sudo apt install docker.io  
(Installing nexus through docker image) 

vi /etc/docker/daemon.json
{
 "insecure-registries":[<your nexus ip>:5000]
}
(As nexus is a insecure link ( http ), we should let know docker about this )
sudo systemctl restart docker
sudo chmod 666 /var/run/docker.sock ( just a workaround instead we should add jenkins to docker group )   
docker run -d -p 8081(host):8081(continer) -p 5000:5000 sonatype/nexus3
```
8081 -- nexus  
5000 -- to private docker registry 

We can access nexus over browser < public ip >:8081 
username : admin   
The password is stored in admin.password file which can be accessed as below :  
```bash
docker ps # get the container name
docker exec -it < container name> /bin/bash
cd sonatype-work/nexus3
cat admin.password
```

Login using username & password to nexus   
setup new password   
Enable anonymous activities ( without creds also anyone can access creds )  

<img width="1504" height="697" alt="image" src="https://github.com/user-attachments/assets/835f6422-0d37-4a61-ad25-cf7b8c52031b" />

Maven-releases : artifacts to deployment (prod)  
maven-snapshots-- artifacts in lower level area ( like dev/test)  

In settings,  
repos -- where we can upload any artifacts
blob -- all the artifacts uploaded
proprietary resources -- security purpose : only belongs to org ( so that url will not be allocated to others )  
security -- user management   
tasks --  policies can be setup 


==================================================================================================================

configuring jenkins & sonarqube ( 2 ec2 instances t2.medium) 
Sonarqube:
```bash
sudo apt update
sudo apt install -y openjdk-17-jdk-headless
sudo apt install docker.io
sudo docker run -d -p 9000:9000 sonarqube:lts-community 
Access sonar at :9000 default access: admin, admin
```

Jenkins
```bash
sudo apt install -y openjdk-17-jdk-headless
vi jenkins.sh
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

chmod +x Jenkins.sh 
./Jenkins.sh
sudo apt update
sudo apt install jenkins
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

Access sonar @ <public-ip>:9000
       Jenkins @ <public-ip>: 8080

==========================================================================================================



    
