pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload_Loans')
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
            stage('ContinuousBuild_Loans')
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
        }
    }
}
