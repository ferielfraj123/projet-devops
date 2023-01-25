pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('bootstrap-dockerhub')
        }
    stages {

        stage('ECHO') {
            steps {
                sh 'echo hello world'
                sh 'ls -lah'
                
            }
        }

      

        
        stage('Deployment') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'k8s', namespace: '', restrictKubeConfigAccess: false, serverUrl: '') {
                    sh'kubectl apply -f manifest/.'
            }
            }
        }
    }
}
