pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('bootstrap-dockerhub')
        }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('ECHO') {
            steps {
                sh 'echo hello world'
                sh 'ls -lah'
                
            }
        }
        
    stage('SonarQube Analysis') {
    environment {
        scannerHome = tool 'SonarQube Scanner'
    }
    steps {
        withCredentials([usernamePassword(credentialsId: 'sonarqube-credentials', usernameVariable: 'SONAR_USER', passwordVariable: 'SONAR_PASSWORD')]) {
            withSonarQubeEnv('SonarQube') {
                sh "${scannerHome}/bin/sonar-scanner -Dsonar.login=${SONAR_USER} -Dsonar.password=${SONAR_PASSWORD}"
            }
        }
    }
}


        stage('Docker Build') {
            steps {
                sh 'docker build -t bahachalbia/catalog:latest microservice-demo/microservice-demo-catalog/'
                sh 'docker build -t bahachalbia/customer:latest microservice-demo/microservice-demo-customer/'
                sh 'docker build -t bahachalbia/eureka:latest microservice-demo/microservice-demo-eureka-server/'
                sh 'docker build -t bahachalbia/order:latest microservice-demo/microservice-demo-order/'
                sh 'docker build -t bahachalbia/turbine:latest microservice-demo/microservice-demo-turbine-server/'
                sh 'docker build -t bahachalbia/zuul:latest microservice-demo/microservice-demo-zuul-server/'
                 }
        }
          stage('login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u bahachalbia --password-stdin '

            }
        }
        stage('push') {
            steps {
                sh 'docker push bahachalbia/catalog'
                sh 'docker push bahachalbia/customer'
                sh 'docker push bahachalbia/eureka'
                sh 'docker push bahachalbia/order'
                sh 'docker push bahachalbia/turbine'
                sh 'docker push bahachalbia/zuul'

            }
        }
        stage('Docker Logout') {
            steps {
                sh 'docker logout'
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
