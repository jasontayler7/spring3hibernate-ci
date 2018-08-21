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
            tool name: 'mvn-3.5.4', type: 'maven'
            sh "mvn clean compile"
        }
    }
}
