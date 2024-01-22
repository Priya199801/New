pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/Priya199801/maven.git'
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
               deploy adapters: [tomcat9(credentialsId: '9dbb4c82-2254-4138-8009-7b425c97c0b5', path: '', url: 'http://172.31.33.13:8080')], contextPath: 'test', war: '**/*.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
               git 'https://github.com/Priya199801/Testing.git'
               sh 'java -jar /home/ubuntu/.jenkins/workspace/Multi_Branch/default/testing.jar'               
            }
        }
       
    }
    
    post
    {
        success
        {
            input message: 'Need approval from the DM!', submitter: 'srinivas'
            deploy adapters: [tomcat9(credentialsId: 'df338e8f-8ae5-4a86-bde2-db80d75548cf', path: '', url: 'http://172.31.36.79:8080')], contextPath: 'test', war: '**/*.war'
        }
        failure
        {
            mail bcc: '', body: 'Continuous Integration has failed', cc: '', from: '', replyTo: '', subject: 'CI Failed', to: 'piaagamanagatti89@gmail.com'
        }
       
    }
       
}
