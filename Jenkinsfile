pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('bootstrap-dockerhub')
        }
    stages {

        stage('login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u bahachalbia --password-stdin '

            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t bahachalbia/catalog /microservice-demo/microservice-demo-catalog/Dockerfile'
                sh 'docker build -t bahachalbia/customer /microservice-demo/microservice-demo-customer/Dockerfile'
                sh 'docker build -t bahachalbia/eureka /microservice-demo/microservice-demo-eureka-server/Dockerfile'
                sh 'docker build -t bahachalbia/order /microservice-demo/microservice-demo-order/Dockerfile'
                sh 'docker build -t bahachalbia/turbine /microservice-demo/microservice-demo-turbine-server/Dockerfile'
                sh 'docker build -t bahachalbia/zuul /microservice-demo/microservice-demo-zuul-server/Dockerfile'
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

    }
}
