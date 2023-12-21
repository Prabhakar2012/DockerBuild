pipeline {
    agent { label 'my_slave'}
       stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Java-Techie-jt/devops-automation']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t prabhakar1978/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                     withCredentials([string(credentialsId: 'MapleDocker', variable: 'dockervar1')]) {
                   sh 'docker login -u prabhakar1978 -p ${dockervar1}'

}
                   sh 'docker push prabhakar1978/devops-integration'
                }
            }
        }
     }
}
