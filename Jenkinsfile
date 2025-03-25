pipeline
{
    agent any

    stages
    {
        stage('Code Checkout')
        {
            steps
            {
                git branch:main, url:'https://github.com/jdo-odoo/igp_mar22.git'
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

        stage('Code compile')
        {
            steps
            {
               sh 'mvn compile'
            }
        }
        
    }
}