pipeline{
    agent any 
    environment{
        VERSION = "${env.BUILD_ID}"
    }
    stages{
        stage("sonar quality check"){
            agent {
                docker {
                    image 'openjdk:11'
                }
            }

        }
        stage("docker build & docker push"){
                    steps{
                        script{
                            withCredentials([string(credentialsId: 'docker_pass', variable: 'docker_password')]) {
                                     sh '''
                                        docker build -t 34.82.95.60:8083/springapp:${VERSION} .
                                        docker login -u admin -p $docker_password 34.82.95.60:8083
                                        docker push  34.82.95.60:8083/springapp:${VERSION}
                                        docker rmi  34.82.95.60:8083/springapp:${VERSION}
                                    '''
                            }
                        }
                    }
                }
       
    }

    
}
