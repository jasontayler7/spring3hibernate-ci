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
            
            withMaven(
        // Maven installation declared in the Jenkins "Global Tool Configuration"
        maven: 'mvn-3.5.4',
        // Maven settings.xml file defined with the Jenkins Config File Provider Plugin
        // Maven settings and global settings can also be defined in Jenkins Global Tools Configuration
        mavenSettingsConfig: 'my-maven-settings',
        mavenLocalRepo: '.repository') {
 
      // Run the maven build
      sh "mvn clean compile"
        }
            
        }
    }
}
