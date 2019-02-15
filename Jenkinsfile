try {
node {
    def app

    stage('Clone Repository')
    {
        checkout scm
    }

    stage('Show me the files') {

        sh "ls -l"	
      
    }
 stage('Apply changes to the environment') {

        sh "ls -l"	
       sh "php -S localhost:5000"
    }


}
} catch(Error|Exception e) {
  //Finish failing the build after telling someone about it
  throw e
} finally {
        // Post build steps here
        /* Success or failure, always run post build steps */
        // send email
        // publish test results etc etc
    }



 /*****************************************
 * To use this function you need to install
 * the Slack Notification Plugin
 ****************************************/

def notifySlack(additionalInfo = '') {
    def colorCode = '#79ae40'
    def status = 'SUCCESS'
    if (currentBuild.result == 'FAILURE') {
        colorCode = '#d34e56'
        status = 'FAILURE'
    }
    if (currentBuild.result == 'ABORTED' ) {
        colorCode = '#938d8e'
        status = 'ABORTED'
    }
    def commitText = sh(returnStdout: true, script: 'git show -s --format=format:"*%s*  _by %an_" HEAD').trim()
    def subject = "${env.JOB_NAME} - #${env.BUILD_NUMBER} ${status} (<${env.BUILD_URL}|Open>)"
    def summary = "${subject}\nChanges: ${commitText}\nBranch: ${env.GIT_BRANCH}\n${additionalInfo}"
    slackSend channel: "${env.SLACK_CHANNEL}", color: colorCode, message: summary, teamDomain: "${env.SLACK_TEAM_DOMAIN}", token: "${env.SLACK_TOKEN}"
}
