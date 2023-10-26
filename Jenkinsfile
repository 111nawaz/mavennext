pipeline {
    agent any
    environment {
        PATH = "/opt/apache-maven-3.9.5/bin:$PATH"
    }
    stages {
        stage('clone code') {
            steps {
                git 'https://github.com/111nawaz/mavennext.git'
            }
        }
        stage("Build code"){
            steps {
                sh "mvn clean install"
            }
        } 
        stage("s3 uplode"){
            steps {
                sh "aws s3 cp /var/lib/jenkins/workspace/ s3://mpocket8 --recursive"
                
            }
        }  
        stage(" uplode"){
            sshagent(['deploy_user']) {
               sh "scp -o  webapp/target/webapp.war ec2-user@3.81.5.92:/opt/apache-tomcat-9.0.82/webapps"
}
                
            }
        } 
    }
}
    
