pipeline
{
    agent any

    environment {
        DOCKER_IMAGE = 'jdossougoin/abc:${BUILD_NUMBER}'
        DOCKER_REGISTRY = 'hub.docker.com'
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
                sh 'docker build -t jdossougoin/abc:${BUILD_NUMBER} .'
                sh 'docker tag jdossougoin/abc:${BUILD_NUMBER} '
            }
        }

        stage('Push Docker Image')
        {
            steps{
                withDockerRegistry([credentialsId: "DockerHub_Credentials", url:"https://${DOCKER_REGISTRY}"]){
                    sh 'docker push jdossougoin/abc:${BUILD_NUMBER}'
                }
            }
        }

        stage('Deploy as container')
        {
            steps{
                sh 'docker run -itd -P jdossougoin/abc:${BUILD_NUMBER}'
            }
        }
        
    }
}