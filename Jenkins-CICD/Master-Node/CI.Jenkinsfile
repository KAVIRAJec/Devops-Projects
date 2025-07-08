pipeline {
    agent any
    
    tools {
        jdk 'jdk11'
        maven 'maven3'
    }

    environment {
        SCANNER_HOME= tool 'sonar-scanner'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/jaiswaladi246/Ekart'
            }
        }
        
        stage('Compile') {
            steps {
                sh "mvn clean compile"
            }
        }
        
        stage('Sonarqube Analysis') {
            steps {
                sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.url=http://127.0.0.1:9000/ -Dsonar.login=squ_0d791964047f6af980b139377fd0d6c0c12c35da -Dsonar.projectName=shopping-cart \
                -Dsonar.java.binaries=. \
                -Dsonar.projectKey=shopping-cart'''
            }
        }
        
        stage('OWASP SCAN') {
            steps {
                dependencyCheck additionalArguments: '--scan ./', odcInstallation: 'DP'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        
        stage('Build Application') {
            steps {
                sh "mvn clean install -DskipTests=true"
            }
        }
        
        stage('Build & Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: '4935269e-0008-436c-b7f1-b9e562298168', toolName: 'docker') {
                        sh "docker build -t shopping:latest -f docker/Dockerfile ."
                        sh "docker tag shopping:latest kaviraj2003/shoppingJenkins:latest"
                        sh "docker push kaviraj2003/shoppingJenkins:latest"
                    }
                }
            }
        }
        
        stage('Trigger CD Pipeline') {
            steps {
                build job: "CD_Pipeline", wait: true
            }
        }
    }
}
