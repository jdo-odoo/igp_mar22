pipeline
{
    agent any

    stages
    {
        stage('Code Checkout')
        {
            steps
            {
                git url:'https://github.com/jdo-odoo/igp_mar22.git'
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
        
    }
}