
go to nexus --> repository --> create --> npm hosted   
name : npm-private
copy thr repo url   
Jenkins -->plugins:  config file provider, nodejs  
tools: nodejs   
managed files: add custom config ( .npmrc)  
id: npmrc, name: .npmrc content: ( need to add repo url & creds here)  
registry=repourl
//<nexus-public-ip>:8081/repository/npm-private/:_auth=<yourauth>  
<yourauth> can be achieved by echo -n 'username:password' | base64

create pipeline:
<img width="1097" height="475" alt="image" src="https://github.com/user-attachments/assets/12fabb01-c630-4182-a024-8a62e77c175d" />

