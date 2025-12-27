pipeline
{
    agent any
    stages
    {
       stage('ContinuousDownload') 
       {
           steps
           {
               git 'https://github.com/IntelliqDevops/maven.git'
           }
     }
       stage('ContinuousBuild')
       {
           steps
           {
               sh 'mvn package'
           }
    
       }
       stage('ContinuousDeploy')
       {
        steps
        {
            deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'e7f8dd0b-320b-431b-88ae-a8f25c43ef91', path: '', url: 'http://172.31.18.19:8080')], contextPath: 'testapp', war: '**/*.war'
        }
     }
     stage('ContinuousTesting')
       {
        steps
        {
            git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
            sh 'java -jar /var/lib/jenkins/workspace/ScriptedPipeline/testing.jar'
        }
     }
     stage('ContinuousDelivery')
       {
        steps
        {
            deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'e7f8dd0b-320b-431b-88ae-a8f25c43ef91', path: '', url: 'http://172.31.20.251:8080')], contextPath: 'prodapp', war: '**/*.war'
        }
     }

    }
}
