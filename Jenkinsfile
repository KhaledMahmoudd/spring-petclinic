pipeline {
    agent any
    
    environment {
        GIT_REPO = 'https://github.com/spring-projects/spring-petclinic.git'
        BRANCH = 'main'
    }
    
    tools {
        maven 'mvn-iti'
    }
    
    stages {
        stage ('Fetch git repo') {
            steps {
                git branch: "${BRANCH}", url: "${GIT_REPO}"
            }
        }
        
        stage ('Change Config') {
            steps {
               sh 'echo "server.port=9090" >> /var/jenkins_home/workspace/Lab/src/main/resources/application.properties'
            }
        }
        
        stage ('Test') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage ('Packing') {
            steps {
                sh 'mvn package -DskipTests'  
            }
        }
        
        stage ('Deploy to Tomcat') {
            steps {
                sh ' nohup java -jar target/*.jar --server.port=9090 > app.log 2>&1 & sleep 100'  
            }
        }
    }
}