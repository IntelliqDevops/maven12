pipeline
{
    agent any
    stages
    {
        stage('Download')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/maven.git'
            }
        }
        stage('Build')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('Deployment')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'c7de6a1f-04db-4ce7-bd96-0d5d5ecedcec', path: '', url: 'http://172.31.22.1:8080')], contextPath: 'mytestapp', war: '**/*.war'
            }
        }
        stage('Testing')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
                
            }
        }
        stage('Delivery')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'c7de6a1f-04db-4ce7-bd96-0d5d5ecedcec', path: '', url: 'http://172.31.30.192:8080')], contextPath: 'myprodapp', war: '**/*.war'
            }
        }
    }
}
