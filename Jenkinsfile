pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('bootstrap-dockerhub')
        }
    stages {

        

        stage('Docker Build') {
            steps {
                sh 'docker build -t bahachalbia/catalog -f /microservice-demo/microservice-demo-catalog/Dockerfile'
                sh 'docker build -t bahachalbia/customer -f /microservice-demo/microservice-demo-customer/Dockerfile'
                sh 'docker build -t bahachalbia/eureka -f /microservice-demo/microservice-demo-eureka-server/Dockerfile'
                sh 'docker build -t bahachalbia/order -f  /microservice-demo/microservice-demo-order/Dockerfile'
                sh 'docker build -t bahachalbia/turbine -f /microservice-demo/microservice-demo-turbine-server/Dockerfile'
                sh 'docker build -t bahachalbia/zuul -f /microservice-demo/microservice-demo-zuul-server/Dockerfile'
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

    }
}
