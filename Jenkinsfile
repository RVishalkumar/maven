pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/sudarshansw7/mymaven.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'c4547938-f333-44ae-829e-f696a0ad8672', path: '', url: 'http://172.31.13.158:8080')], contextPath: 'test', war: '**/*.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                git 'https://github.com/sudarshansw7/myfunctionaltesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'c4547938-f333-44ae-829e-f696a0ad8672', path: '', url: 'http://172.31.14.248:8080')], contextPath: 'prod', war: '**/*.war'
            }
        }
    }
}
