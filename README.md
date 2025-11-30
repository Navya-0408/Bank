# Bank   this is navya
1)Nagios
2)Kubernets
3)AWS
4)Jenkins Pipeline
5)Maven Java
6)Docker CLI Commands
7)Jenkins Maven-Java
8)Jenkins maven-web




===nagios==
 docker pull jasonrivers/nagios:latest
 docker images
 docker run --name nagios4 -d -p 8888:80 jasonrivers/nagios:latest
 docker start -ai nagios4
 *open browser type localhost:8888
     username: nagiosadmin
     pw: nagios

===kubernets===
minikube start
docker login
minikube version
minikube status
kubectl create deployment myngnix --image=ngnix
kubectl get deployment
kubectl get pods
kubectl describe pods 
kubectl expose deployment myngnix --type-Nodeport --port=80 --target-port=80 --name=myngnix
kubectl get service myngnix
kubectl port-forward sevice/myngnix 3080:80
openbrowser and in url 127.0.0.1-3080
....
then open another powershell and 
minikube dashboard



===AWS===
goto AWS
goto Modules
Click- Launch AWS Academy Learner Lab
click- Start Lab
click- AWS->EC2 -> goto Instances-> click- Launch Instances
Name-> MyAws ->select ubuntu
click- Create new key pair->enter name-> Create key pair
select radio buttons -> Launch Instances.
come to Instances ->select what uh created->click-> connect->copy link
Go to Folder->create new Folder -> paste downloaded file
goto cmd via path ->paste link ,type yes
install all this :
sudo apt update
sudo apt-get install docker.io -y
sudo apt install git -y
sudo apt install nano -y
then open git select AWS goto to code->copy link 
in cmd ->git clone copy link
-> cd aws
nano Dockerfile
->
FROM nginx
COPY . /usr/share/nginx/html
Save: Ctrl + O → Enter → Ctrl + X
sudo docker build -t mywebapp .
sudo docker run -d -p 80:80 mywebapp
 Go to EC2->select Instances ->Copy IPv4 addess
paste in browser
DONE



======Jenkins Pipeline Steps======
+New Item -> enter item name "pipeline-Navya"
under that-> click pipeline  -> ok
paste this code
pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Cloning java-hello-world-with-maven repo'
                git branch: 'master', url: 'https://github.com/jabedhasan21/java-hello-world-with-maven.git'
            }
        }

        stage('Clean') {
            steps {
                echo 'Running mvn clean'
                bat "mvn clean"
            }
        }

        stage('Compile') {
            steps {
                echo 'Running mvn compile'
                bat "mvn compile"
            }
        }

        stage('Test') {
            steps {
                echo 'Running mvn test'
                bat "mvn test"
            }
        }

        stage('Package') {
            steps {
                echo 'Running mvn package'
                bat "mvn package"
            }
        }

        stage('Archive Artifact') {
            steps {
                echo 'Archiving JAR output'
                archiveArtifacts artifacts: "target/*.jar", fingerprint: true
            }
        }
    }

    post {
        success {
            echo '🎉 BUILD SUCCESS — JAR created and archived ✔'
        }
        failure {
            echo '❌ BUILD FAILED'
        }
    }
}    
click  Apply then save
click Build Now
click on green right symbol then click on pipeline overview  
DONE


===Maven java===
1️⃣ Check Maven Version
Steps

Press Windows + R

Type: cmd

Click OK

Type:

mvn -version


Press Enter

If you get 'mvn' not recognized → Maven not installed or PATH not added.

2️⃣ Create Maven Java Project (Using Eclipse)
Steps

Open Eclipse IDE

On top menu → click File

Click New

Click Project…

Expand Maven

Click Maven Project

Click Next

Check Create a simple project (skip archetype selection)

Click Next

Fill details:

Field	Value
Group Id	maven_java
Artifact Id	java_maven
Version	0.0.1-SNAPSHOT
Packaging	jar

Click Finish

3️⃣ Maven Java Project Structure (as shown in PDF)

In Project Explorer, you will see:

src/main/java  
src/test/java  
pom.xml  


No action needed — Eclipse creates it automatically.

4️⃣ Run the Java Program (Output in PDF)
Steps

Right-click src/main/java

Click New → Class

Enter:

Name: Demo     click:finish

Paste sample code:

public class Demo {
    public static void main(String[] args) {
        System.out.println("Maven Java Project");
    }
}        save with ctrl+s


Right-click on the file → Run As → Java Application     ---->>>MAVEN_JAVA

Click New Repository (green button or “+” → “New repository”)                        
 Click Create Repository                                                                                                      
 Open your project folder in Terminal / PowerShell                                                      
 git init                                                                                                 
 git add .
 git commit -m "Initial Maven project commit"                                                                                                
 git remote add origin https://github.com/Navya-0408/my-maven-java-project.git                                                                                       git branch -M main
git push -u origin main
 DONE


 ===Docker CLI Commands===
 docker pull redis 
docker run --name my-redis -d redis 
docker ps 
docker exec -it my-redis redis-cli  
 docker stop my-redis
docker start my-redis 
docker rm my-redis  
docker rmi redis
docker run --name my-redis -d redis 
docker ps 
 docker logs my-redis 
docker network ls 
docker network create mynet 
docker run -d --name redis-server --network=mynet redis 
docker volume create mydata 
docker volume ls 
docker volume inspect mydata 
docker run -d --name my-reds -v mydata:/data redis 
docker rmi image-name 
docker pull redis



# jenkins
===steps for MavenJava Automation:===
Maven Java Automation Steps:
 Step 1: Open Jenkins (localhost:8080)
   	 ├── Click on "New Item" (left side menu
Step 2: Create Freestyle Project (e.g., MavenJava_Build)
        	├── Enter project name (e.g., MavenJava_Build)
        	├── Click "OK".
└── Configure the project:
            		├── Description: "Java Build demo"
            		├── Source Code Management:
            			└── Git repository URL: [GitMavenJava repo URL]   
               url1:-->https://github.com/Navya-0408/my-maven-java-project.git
               url:https://github.com/jabedhasan21/java-hello-world-with-maven
            		├── Branches to build: */Main
  		└── Build Steps:
               	     ├── Add Build Step -> "Invoke top-level Maven targets"
                  		└── Maven version: MAVEN_HOME
                 		└── Goals: clean
                	├── Add Build Step -> "Invoke top-level Maven targets"
                		└── Maven version: MAVEN_HOME
                		└── Goals: install.
                	└── Post-build Actions:
                    	       ├── Add Post Build Action -> "Archive the artifacts"
                    			└── Files to archive: */
                    	     ├── Add Post Build Action -> "Build other projects"
                    			└── Projects to build: MavenJava_Test
                    			└── Trigger: Only if build is stable
                    	     └── Apply and Save


    └── Step 3: Create Freestyle Project (e.g., MavenJava_Test)
        	├── Enter project name (e.g., MavenJava_Test)
        	├── Click "OK"
              └── Configure the project:
             ├── Description: "Test demo"
             ├── Build Environment:
            		└── Check: "Delete the workspace before build starts"
            ├── Add Build Step -> "Copy artifacts from another project"
            		└── Project name: MavenJava_Build
            		└── Build: Stable build only  // tick at this
            		└── Artifacts to copy: */
            ├── Add Build Step -> "Invoke top-level Maven targets"
            		└── Maven version: MAVEN_HOME
            		└── Goals: test
            		└── Post-build Actions:
                ├── Add Post Build Action -> "Archive the artifacts"
                	└── Files to archive: */
                	└── Apply and Save

    └── Step 4: Create Pipeline View for Maven Java project
        ├── Click "+" beside "All" on the dashboard
        ├── Enter name: MavenJava_Pipeline
        ├── Select "Build pipeline view"         // tick here
         |--- create
        └── Pipeline Flow:
            ├── Layout: Based on upstream/downstream relationship
            ├── Initial job: MavenJava_Build
            └── Apply and Save OK

    └── Step 5: Run the Pipeline and Check Output
        ├── Click on the trigger to run the pipeline
        ├── click on the small black box to open the console to check if the build is success




 maven_we automation steps:
=== II. Maven Web Automation Steps:====
└── Step 1: Open Jenkins (localhost:8080)
    ├── Click on "New Item" (left side menu)
    
    └── Step 2: Create Freestyle Project (e.g., MavenWeb_Build)
        ├── Enter project name (e.g., MavenWeb_Build)
        ├── Click "OK"
        └── Configure the project:
            ├── Description: "Web Build demo"
            ├── Source Code Management:
            		└── Git repository URL: [GitMavenWeb repo URL]
              url:-->https://github.com/MithunTechnologiesDevOps/maven-web-application.git 
            ├── Branches to build: */Main or master
            └── Build Steps:
                ├── Add Build Step -> "Invoke top-level Maven targets"
                	└── Maven version: MAVEN_HOME
                	 └── Goals: clean
                ├── Add Build Step -> "Invoke top-level Maven targets"
                	└── Maven version: MAVEN_HOME
                	└── Goals: install
                └── Post-build Actions:
                    ├── Add Post Build Action -> "Archive the artifacts"
                   	 └── Files to archive: */
                    ├── Add Post Build Action -> "Build other projects"
                    	└── Projects to build: MavenWeb_Test
                    	└── Trigger: Only if build is stable
                    └── Apply and Save

    └── Step 3: Create Freestyle Project (e.g., MavenWeb_Test)
        ├── Enter project name (e.g., MavenWeb_Test)
        ├── Click "OK"
        └── Configure the project:
            ├── Description: "Test demo"
            ├── Build Environment:
            		└── Check: "Delete the workspace before build starts"
            ├── Add Build Step -> "Copy artifacts from another project"
            		└── Project name: MavenWeb_Build
            		└── Build: Stable build only
            		└── Artifacts to copy: */
            ├── Add Build Step -> "Invoke top-level Maven targets"
           		└── Maven version: MAVEN_HOME
            		└── Goals: test
            └── Post-build Actions:
                ├── Add Post Build Action -> "Archive the artifacts"
                	└── Files to archive: */
                ├── Add Post Build Action -> "Build other projects"
                	└── Projects to build: MavenWeb_Deploy
                └── Apply and Save

    └── Step 4: Create Freestyle Project (e.g., MavenWeb_Deploy)
        ├── Enter project name (e.g., MavenWeb_Deploy)
        ├── Click "OK"
        └── Configure the project:
            ├── Description: "Web Code Deployment"
            ├── Build Environment:
            		└── Check: "Delete the workspace before build starts"
            ├── Add Build Step -> "Copy artifacts from another project"
            		└── Project name: MavenWeb_Test
            		└── Build: Stable build only
               	└── Artifacts to copy: */
            └── Post-build Actions:
                ├── Add Post Build Action -> "Deploy WAR/EAR to a container"
   └── WAR/EAR File: */.war
   └── Context path: Webpath
 └── Add container -> Tomcat 9.x remote
└── Credentials: Username: admin, Password: 1234
── Tomcat URL: https://localhost:8085/
------deploy on failure tick here also 

                └── Apply and Save

    └── Step 5: Create Pipeline View for MavenWeb
        ├── Click "+" beside "All" on the dashboard
        ├── Enter name: MavenWeb_Pipeline
        ├── Select "Build pipeline view"
        └── Pipeline Flow:
            ├── Layout: Based on upstream/downstream relationship
            ├── Initial job: MavenWeb_Build
            └── Apply and Save

    └── Step 6: Run the Pipeline and Check Output
        ├── Click on the trigger “RUN” to run the pipeline
url--??https://github.com/MithunTechnologiesDevOps/maven-web-application.git
     
