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
}
}
