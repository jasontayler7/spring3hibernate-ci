ansiColor('xterm') {
    properties ([
        buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '10')),
        [$class: 'RebuildSettings', autoRebuild: false, rebuildDisabled: false],
        disableConcurrentBuilds(),
    ])

    def config = [:]
    node {
        stage("Checkout the latest code of Repo")
        {
            checkout scm
            echo "Listing all repo content"
            sh "ls -l"
            sh "whoami"
        }
        stage("checking codestability")
        {
            
                withEnv(['JAVA_HOME=${ tool \'java-8\' }', 'PATH+MAVEN=${tool \'mvn-3.5.4\'}/bin:${env.JAVA_HOME}/bin']) {
                    sh "mvn compile"
            }
            
        }
    }
}
