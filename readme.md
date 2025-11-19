**Minikube10**



curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-installer.exe

.\\minikube-installer.exe



minikube start --driver=docker



kubectl create deployment mynginx --image=nginx



kubectl get pods

kubectl get deployments

kubectl describe pods



kubectl expose deployment mynginx --type=NodePort --port=80 --target-port=80

kubectl get service mynginx



kubectl scale deployment mynginx --replicas=4



kubectl port-forward svc/mynginx 8081:80

http://localhost:8081



minikube dashboard

kubectl delete deployment mynginx

kubectl delete service mynginx

minikube stop

minikube delete





**Nagios10**



docker pull jasonrivers/nagios:latest

docker run --name nagiosdemo -p 8888:80 jasonrivers/nagios:latest

http://localhost:8888

Username: nagiosadmin

Password: nagios

docker stop nagiosdemo

docker rm nagiosdemo

docker rmi jasonrivers/nagios:latest



**AWS12**



Create instance , take the ssh command, 



icacls "D:\\aws\\MyExampleKeyPair.pem" /remove "BUILTIN\\Users"

icacls "D:\\aws\\MyExampleKeyPair.pem" /remove "Everyone"

whoami

icacls "D:\\aws\\MyExampleKeyPair.pem" /grant:r Admin:R



paste in terminal



sudo apt update

sudo apt-get install docker.io

sudo apt install git

sudo apt install nano

clone

cd

nano Dockerfile

sudo docker build -t img1 .

sudo docker run -d -p 8000:80 img1



instances->ipv4 address -> paste ip in url



dockerfile(index.html)

FROM nginx:alpine

COPY . /usr/share/nginx/html



dockerfile(webapp)

FROM tomcat:9-jdk11

COPY target/\*.war /usr/local/tomcat/webapps





**ngrok11**



EXERCISE 1 — Jenkins CI/CD using Git Webhook

Step 1: Install Ngrok

Open Settings → Privacy \& Security → Windows Security

Turn Antivirus OFF temporarily.

Step 2: Sign Up on Ngrok

Go to: https://ngrok.com

Sign up using name, email, and a 10+ character password.

Step 3: Download Ngrok

After login → top-left shows your name.

Click Download for Windows (64-bit).

Step 4: Extract \& Run

Extract ZIP

Double-click ngrok.exe

Ngrok terminal will open.

Step 5: Connect Ngrok Account

Go to Dashboard → Your Authtoken

Copy the token.

In Ngrok terminal run:

ngrok config add-authtoken <your\_token>

Step 6: Start a Tunnel for Jenkins

Check Jenkins port:

Open browser → http://localhost:8081

Start tunnel:

ngrok http 8081

Copy the public HTTPS URL (example):

https://unhired-stormily-alaine.ngrok-free.dev

Step 7: Configure GitHub Webhook

Open your GitHub Repo

Settings → Webhooks → Add Webhook

Payload URL:

https://<your-ngrok-url>/github-webhook/

Example:

https://unhired-stormily-alaine.ngrok-free.dev/github-webhook/

Set Content Type → application/json

Select → Just the Push Event

Click Add Webhook

Step 8: Configure Jenkins Build Trigger

Open Jenkins

Select your Job → Configure

Under Build Triggers

✔ Check: GitHub hook trigger for GITScm polling

Save

Step 9: Test

Push any code change to GitHub

GitHub triggers webhook

Jenkins auto-starts build

Outcome

GitHub → Ngrok → Jenkins

Push = Auto-build

⭐ FIX FOR YOUR ERROR

"Error fetching file… and Build didn’t start automatically"

This happens when:

✔ Ngrok tunnel expired

✔ Wrong webhook URL

✔ Jenkins not exposed

✔ GitHub cannot reach localhost

Fix:

Make sure Ngrok is running when you push

Use the HTTPS ngrok URL

Webhook must end with:

/github-webhook/

In Jenkins job → Build Triggers → GitHub hook trigger must be enabled.

EXERCISE 2 — Jenkins Email Notification Setup

Step 1: Create Gmail App Password

Go to https://myaccount.google.com

Security → 2-Step Verification → Turn ON

Go to:

Security → App Passwords

Select:

App = Other

Name = Jenkins

Generate → Copy the 16-digit password.

Step 2: Install Plugin

Manage Jenkins → Manage Plugins → Available

Install:

✔ Email Extension Plugin

✔ Mailer Plugin

Restart Jenkins.

Step 3: Configure Email in Jenkins

A. Go to:

Manage Jenkins → Configure System

Scroll to E-mail Notification (NOT Editable Email Notification)

Expand Advanced, then fill in:

Field	Value

SMTP Server	smtp.gmail.com

Use SMTP Authentication	✔

Username	your Gmail

Password	16-digit App Password

Use SSL	✔

SMTP Port	465

Click Test Configuration.

B. Extended Email Notification (optional)

Set the same SMTP server + port.

Step 4: Configure Email in a Job

Your Job → Configure → Post-build Actions →

Editable Email Notification

Set:

Project Recipient List → your email

Trigger → e.g., Failure or Success

Save.



**jenkins8**



I. Steps for MavenJava Automation:

Maven Java Automation Steps:

Step 1: Open Jenkins (localhost:8080)

├── Click on "New Item" (left side menu

Step 2: Create Freestyle Project (e.g., MavenJava\_Build)

├── Enter project name (e.g., MavenJava\_Build)

├── Click "OK"

└── Configure the project:

├── Description: "Java Build demo"

├── Source Code Management:

└── Git repository URL: \[GitMavenJava repo URL]

├── Branches to build: \*/Main or \*/master

└── Build Steps:

├── Add Build Step -> "Invoke top-level Maven targets"

└── Maven version: MAVEN\_HOME

└── Goals: clean

├── Add Build Step -> "Invoke top-level Maven targets"

└── Maven version: MAVEN\_HOME

└── Goals: install

└── Post-build Actions:

├── Add Post Build Action -> "Archive the artifacts"

└── Files to archive: \*\*/\*

├── Add Post Build Action -> "Build other projects"

└── Projects to build: MavenJava\_Test

└── Trigger: Only if build is stable

└── Apply and Save

└── Step 3: Create Freestyle Project (e.g., MavenJava\_Test)

├── Enter project name (e.g., MavenJava\_Test)

├── Click "OK"

└── Configure the project:

├── Description: "Test demo"

├── Build Environment:

└── Check: "Delete the workspace before build starts"

├── Add Build Step -> "Copy artifacts from another project"

└── Project name: MavenJava\_Build

└── Build: Stable build only // tick at this

└── Artifacts to copy: \*\*/\*

├── Add Build Step -> "Invoke top-level Maven targets"

└── Maven version: MAVEN\_HOME

└── Goals: test

└── Post-build Actions:

├── Add Post Build Action -> "Archive the artifacts"

└── Files to archive: \*\*/\*

└── Apply and Save

└── Step 4: Create Pipeline View for Maven Java project

├── Click "+" beside "All" on the dashboard

├── Enter name: MavenJava\_Pipeline

├── Select "Build pipeline view" // tick here

|--- create

└── Pipeline Flow:

├── Layout: Based on upstream/downstream relationship

├── Initial job: MavenJava\_Build

└── Apply and Save OK

└── Step 5: Run the Pipeline and Check Output

├── Click on the trigger to run the pipeline

├── click on the small black box to open the console to check if the build is success

Note :

1\. If build is success and the test project is also automatically triggered with name

“MavenJava\_Test”

2\. The pipeline is successful if it is in green color as shown ->check the console of the test project

3\. The test project is successful and all the artifacts are archived successfully

II. Maven Web Automation Steps:

└── Step 1: Open Jenkins (localhost:8080)

├── Click on "New Item" (left side menu)

└── Step 2: Create Freestyle Project (e.g., MavenWeb\_Build)

├── Enter project name (e.g., MavenWeb\_Build)

├── Click "OK"

└── Configure the project:

├── Description: "Web Build demo"

├── Source Code Management:

└── Git repository URL: \[GitMavenWeb repo URL]

├── Branches to build: \*/Main or master

└── Build Steps:

├── Add Build Step -> "Invoke top-level Maven targets"

└── Maven version: MAVEN\_HOME

└── Goals: clean

├── Add Build Step -> "Invoke top-level Maven targets"

└── Maven version: MAVEN\_HOME

└── Goals: install

└── Post-build Actions:

├── Add Post Build Action -> "Archive the artifacts"

└── Files to archive: \*\*/\*

├── Add Post Build Action -> "Build other projects"

└── Projects to build: MavenWeb\_Test

└── Trigger: Only if build is stable

└── Apply and Save

└── Step 3: Create Freestyle Project (e.g., MavenWeb\_Test)

├── Enter project name (e.g., MavenWeb\_Test)

├── Click "OK"

└── Configure the project:

├── Description: "Test demo"

├── Build Environment:

└── Check: "Delete the workspace before build starts"

├── Add Build Step -> "Copy artifacts from another project"

└── Project name: MavenWeb\_Build

└── Build: Stable build only

└── Artifacts to copy: \*\*/\*

├── Add Build Step -> "Invoke top-level Maven targets"

└── Maven version: MAVEN\_HOME

└── Goals: test

└── Post-build Actions:

├── Add Post Build Action -> "Archive the artifacts"

└── Files to archive: \*\*/\*

├── Add Post Build Action -> "Build other projects"

└── Projects to build: MavenWeb\_Deploy

└── Apply and Save

└── Step 4: Create Freestyle Project (e.g., MavenWeb\_Deploy)

├── Enter project name (e.g., MavenWeb\_Deploy)

├── Click "OK"

└── Configure the project:

├── Description: "Web Code Deployment"

├── Build Environment:

└── Check: "Delete the workspace before build starts"

├── Add Build Step -> "Copy artifacts from another project"

└── Project name: MavenWeb\_Test

└── Build: Stable build only

└── Artifacts to copy: \*\*/\*

└── Post-build Actions:

├── Add Post Build Action -> "Deploy WAR/EAR to a container"

└── WAR/EAR File: \*\*/\*.war

└── Context path: Webpath

└── Add container -> Tomcat 9.x remote

└── Credentials: Username: admin, Password: 1234

── Tomcat URL: https://localhost:8085/

└── Apply and Save

└── Step 5: Create Pipeline View for MavenWeb

├── Click "+" beside "All" on the dashboard

├── Enter name: MavenWeb\_Pipeline

├── Select "Build pipeline view"

└── Pipeline Flow:

├── Layout: Based on upstream/downstream relationship

├── Initial job: MavenWeb\_Build

└── Apply and Save

└── Step 6: Run the Pipeline and Check Output

├── Click on the trigger “RUN” to run the pipeline

Note:

1\. After Click on Run -> click on the small black box to open the console to check if the build is success

2\. Now we see all the build has success if it appears in green color

├── Open Tomcat homepage in another tab

├── Click on the "/webpath" option under the manager app





**pipeline script9**

Scripted Jenkins Pipeline (Full Procedure + SBQ Answers)

1\. Create Pipeline Job

\- Open Jenkins ® New Item ® Pipeline ® OK.

\- Add description.

2\. Build Triggers

Choose: GitHub hook, Poll SCM, or Schedule (CRON).

3\. Pipeline Script

Definition ® Pipeline Script ® paste fixed script.

4\. Corrected Working Pipeline Code

---

pipeline {

agent any

tools {

jdk 'JAVA-17'

maven 'MAVEN-HOME'

}

stages {

stage('git repo \& clean') {

steps {

bat "rmdir /s /q maven\_java

bat "git clone https://github.com/srinidhikasetty/maven\_java.git"

bat "mvn clean -f maven\_java"

}

}

stage('install') {

steps {

bat "mvn install -f maven\_java"

}

}

stage('test') {

steps {

bat "mvn test -f maven\_java"

}

}

stage('package') {

steps {

bat "mvn package -f maven\_java"

bat "rmdir /s /q maven\_java"

}

}

}

}

