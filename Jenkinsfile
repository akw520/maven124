pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                script
                {
                   try
                   {
                       git 'https://github.com/selenium-saikrishna/maven.git'
                   }
                    catch(Exception e1)
                   {
                        mail bcc: '', body: 'Jenkins is unable to download the dev code from github', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'git.team@gmail.com'
                        exit(1)
                   }
                }
                git 'https://github.com/selenium-saikrishna/maven.git'
            }
        }
            stage('ContinuousMaster')
        {
            steps
            {
                script
                {
                    try
                    {
                        
                    }
                    catch(Exception e2)
                    {
                        mail bcc: '', body: 'Jenkins is unable to create an artificat from the downloaded code', cc: '', from: '', replyTo: '', subject: 'Build Failed', to: 'developers@gmail.com'
                    }
                }
                sh 'mvn package'
            }
        }
            stage('ContinuousDeployment_Master')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '00a3a52f-4aa2-4dcd-a43b-b8b210c5d9e0', path: '', url: 'http://172.31.28.106:8080')], contextPath: 'testapp', war: '**/*.war'
                    }
                    catch(Exception e3)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy artifact into tomcat on the QA Servers', cc: '', from: '', replyTo: '', subject: 'Deployment Failed', to: 'middlewareteam@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousTesting_Master')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/selenium-saikrishna/FunctionalTesting.git'
                        sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline2/testing.jar'
                    }
                    catch(Exception e4)
                    {   
                        mail bcc: '', body: 'Jenkins is unable to deploy artifact into tomcat on the QA Servers', cc: '', from: '', replyTo: '', subject: 'Testing Failed', to: 'qa.team@gmail.com'
                        exit(1)
                    }
            }
        }
         stage('ContinuousDelivery')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '00a3a52f-4aa2-4dcd-a43b-b8b210c5d9e0', path: '', url: 'http://172.31.29.125:8080')], contextPath: 'prodapp', war: '**/*.war'
                    }
                    catch(Exception e5)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy artifact into tomcat on the prod Servers', cc: '', from: '', replyTo: '', subject: 'Delivery Failed', to: 'delivery@gmail.com'
                    }
                }
                
            }
        }
    }
}
