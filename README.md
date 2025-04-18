# Task-08
Elevate Labs

# Jenkins + Maven + Tomcat Deployment (JSP Project)

This project automates the process of setting up a CI/CD pipeline using Jenkins, Maven, and Apache Tomcat to deploy a JSP web application from GitHub.

---

## 📁 Project Structure

- **setup_jenkins_maven_tomcat.sh**  
  Bash script to install Java, Maven, Jenkins, and Tomcat, configure the Tomcat service, and start all services.

- **Jenkinsfile**  
  Jenkins pipeline script to clone a GitHub repo, build it using Maven, and deploy the WAR to Tomcat.

---

## ⚙️ Setup Instructions

### 1. Clone or copy the script

```bash
nano setup_jenkins_maven_tomcat.sh
Paste the content from the provided setup script.

2. Make the script executable and run
bash
Copy
Edit
chmod +x setup_jenkins_maven_tomcat.sh
./setup_jenkins_maven_tomcat.sh
3. Give Jenkins passwordless sudo access
bash
Copy
Edit
sudo visudo
Add this line at the end:

bash
Copy
Edit
jenkins ALL=(ALL) NOPASSWD: ALL
🛠 Jenkins Pipeline Configuration
Use the following Jenkinsfile:
groovy
Copy
Edit
pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Faisalkhan45/APPLICATIONJSP.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh 'sudo cp target/*.war /opt/tomcat/webapps/'
            }
        }
    }
}
🌐 Access Jenkins and Tomcat
Jenkins: http://localhost:8080
Use this to set up Jenkins initially. Password:

bash
Copy
Edit
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Tomcat: http://localhost:9090 or your configured port
App deployed under ROOT context or as APPLICATIONJSP-1.0-SNAPSHOT.
