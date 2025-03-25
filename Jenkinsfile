pipeline
{
    agent any
    stages
    {
        stage('Code Checkout')
        {
            steps
            {
                git 'https://github.com/jdo-odoo/igp_mar22.git'
            }   
        }

        stage('Code compile')
        {
            steps
            {
                mvn  compile
            }
        }

        stage('Code test')
        {
            steps
            {
                mvn  test
            }
        }

        stage('Code packagin')
        {
            steps
            {
                mvn  package
            }
        }
        
    }
}