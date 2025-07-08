pipeline {
    agent {
        docker {
            image 'maven:3.9.5-eclipse-temurin-11-alpine'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    
    environment {
        SCANNER_HOME = "${WORKSPACE}/sonar-scanner"
        ODC_HOME = "${WORKSPACE}/dependency-check"
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/jaiswaladi246/Ekart'
            }
        }
        
        stage('Install Sonar Scanner') {
            steps {
                sh '''
                    curl -sL https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006-linux.zip -o sonar-scanner.zip
                    unzip -q sonar-scanner.zip -d .
                    mv sonar-scanner-* sonar-scanner
                    chmod +x sonar-scanner/bin/sonar-scanner
                '''
            }
        }
        stage('Compile') {
            steps {
                sh "mvn clean compile"
            }
        }
        
        stage('Sonarqube Analysis') {
            steps {
                sh '''
                    ${SCANNER_HOME}/bin/sonar-scanner \
                    -Dsonar.projectKey=shopping-cart \
                    -Dsonar.projectName=shopping-cart \
                    -Dsonar.sources=. \
                    -Dsonar.java.binaries=. \
                    -Dsonar.host.url=http://127.0.0.1:9000 \
                    -Dsonar.login=squ_0d791964047f6af980b139377fd0d6c0c12c35da
                '''
            }
        }
        
        stage('Install OWASP Dependency Check') {
            steps {
                sh '''
                    curl -sL https://github.com/jeremylong/DependencyCheck/releases/download/v9.0.7/dependency-check-9.0.7-release.zip -o odc.zip
                    unzip -q odc.zip -d .
                    mv dependency-check-9.0.7 dependency-check
                    chmod +x dependency-check/bin/dependency-check.sh
                '''
            }
        }
        
        stage('OWASP SCAN') {
            steps {
                sh '''
                    ${ODC_HOME}/bin/dependency-check.sh \
                    --scan ./ \
                    --format XML \
                    --out dependency-check-report.xml
                '''
            }
        }
        
        stage('Build Application') {
            steps {
                sh "mvn clean install -DskipTests=true"
            }
        }
        
        stage('Test Docker Access') {
            steps {
                sh "which docker && docker version"
            }
        }

        stage('Build & Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: '4935269e-0008-436c-b7f1-b9e562298168', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                        docker build -t shopping:latest -f docker/Dockerfile .
                        docker tag shopping:latest kaviraj2003/shoppingJenkins:latest
                        docker push kaviraj2003/shoppingJenkins:latest
                    '''
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
