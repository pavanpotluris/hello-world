node {
    def mvnHome
    stage('GetLatestSourceCodes') { // for display purposes
        // Get some code from a GitHub repository
        git changelog: false, credentialsId: 'JenkinsUser', poll: false, url: 'https://github.com/pavanpotluris/hello-world.git'
        echo "Successfully pulled latest codes from GITHUB"
        mvnHome = tool 'M2_HOME'
    }
    stage('Build') {
        // Run the maven build
        withEnv(["MVN_HOME=$mvnHome"]) {
            if (isUnix()) {
                echo "This is Unix Agent"
                echo "$MVN_HOME"
                echo "$PATH"
                sh 'pwd'
                sh 'whoami'
                sh 'mvn clean install package'
            } else {
                echo "This is Windows Agent"
                bat(/"%MVN_HOME%\opt\maven" -Dmaven.test.failure.ignore clean install package/)
            }
        }
    }
}
