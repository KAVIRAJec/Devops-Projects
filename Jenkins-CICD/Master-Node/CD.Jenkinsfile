pipeline {
    agent any

    stages {
        stage('Docker Deploy to Container') {
            steps {
                script{
                    withDockerRegistry(credentialsId: '4935269e-0008-436c-b7f1-b9e562298168', toolName: 'docker') {
                        sh "docker run -d --name shopping-cart -p 8070:8070 kaviraj2003/shoppingJenkins:latest"
                    }
                }
            }
        }
    }
}
