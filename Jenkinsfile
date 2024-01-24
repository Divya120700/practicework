pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                script {
                    //dockerImage = docker.build("docker-image:latest")
                    sh "docker build . -t  docker-image:latest"
                }
                script {
                    sh "docker run -d -p 8090:80 docker-image:latest"
                    }
                }
            
        }
      stage('testing container') 
       {
        steps
         {
         script
         {
             sh 'sleep 10'
             sh "curl http:// 10.196.153.137:8090"
         }
     }
}

        
    }
}
