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
      
    
