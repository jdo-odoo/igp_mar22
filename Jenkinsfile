pipeline
{
    agent any

    environment {
        DOCKER_REPO = 'jdossougoin/abc'
        DOCKER_LOGIN_ENDPOINT = 'index.docker.io/v1/'
        DOCKER_REGISTRY = 'docker.io/jdossougoin/abc'
    }

    stages
    {
        stage('Code Checkout')
        {
            steps
            {
                git branch:'main',url:'https://github.com/jdo-odoo/igp_mar22.git'
            }   
        }

        stage('Code compile')
        {
            steps
            {
               sh 'mvn compile'
            }
        }

        stage('Code test')
        {
            steps
            {
               sh 'mvn test'
            }
        }

        stage('Code packaging')
        {
            steps
            {
               sh 'mvn package'
            }
        }

        stage('Build Docker Image')
        {
            steps{
                sh 'cp /var/lib/jenkins/workspace/$JOB_NAME/target/ABCtechnologies-1.0.war /var/lib/jenkins/workspace/$JOB_NAME/abc.war'
                sh 'docker build -t abc:${BUILD_NUMBER} .'
                sh 'docker tag abc:${BUILD_NUMBER} ${DOCKER_REPO}:${BUILD_NUMBER}'
                sh 'docker tag abc:${BUILD_NUMBER} ${DOCKER_REPO}:latest'
            }
        }

        stage('Push Docker Image')
        {
            steps{
                withCredentials([string(credentialsId: 'docker_hub_token', variable: 'DOCKER_TOKEN')]) {
                    sh 'echo $DOCKER_TOKEN | docker login -u jdossougoin --password-stdin'
                    sh 'docker push ${DOCKER_REPO}:${BUILD_NUMBER}'
                    sh 'docker push ${DOCKER_REPO}:latest'
                }
            }
        }

        stage('Deploy as container')
        {
            steps{
                sh 'docker run -itd -P ${DOCKER_REPO}:latest'
            }
        }

        stage('Deploy to kubernetes')
        {
            steps{
                sh 'docker run -itd -P ${DOCKER_REPO}:${BUILD_NUMBER}'
            }
        }
        
    }
}