pipeline
{
    agent any
    environment {
    gpg_secret = credentials("gpg-secret")
    gpg_trust = credentials("gpg-ownertrust")
    gpg_passphrase = credentials("gpg-secret-id")
}
    stages
    {
        stage('SCM')
        {
            steps
            {
                git branch: 'main', url: 'https://github.com/Venkatesh37/git-secrets-37.git'
            }
        }
        stage('ImportingTHE GPG')
        {
            steps
            {
                 sh """
        gpg --batch --import $gpg_secret
        gpg --import-ownertrust $gpg_trust
         """
            }
        }
        stage("PrintingTHE Password")
        {
            steps
            {
               
           sh """
                 cd $WORKSPACE
                git secret reveal -p '$gpg_passphrase'
                git secret cat password-37.tax
            """

            }
        }
    }
}
   
