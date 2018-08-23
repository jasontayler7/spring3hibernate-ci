ansiColor('xterm') {
    properties ([
        buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '10')),
        [$class: 'RebuildSettings', autoRebuild: false, rebuildDisabled: false],
        disableConcurrentBuilds(),
    ])

    def config = [:]
    node {
        stage("Checkout the latest code of Repo") {
            checkout scm
            echo "Listing all repo content"
            sh "ls -l"
            sh "whoami"
        }

        stage("checking Code Stability") {
            // Run the maven compile
            sh "cd Spring3HibernateApp/; mvn compile"
        }

        stage("checking Code Quality") {
            // Run the maven findbugs and checkstyle
            sh "cd Spring3HibernateApp/; mvn findbugs:findbugs; mvn checkstyle:checkstyle"
        }

        stage("checking Code Analysis") {
            // Run the maven findbugs and checkstyle
            sh "cd Spring3HibernateApp/; mvn cobertura:cobertura; mvn install"
        }

       stage("deploying, restarting the server") {
            // Deployement on Tomcat server
            sh "cd Spring3HibernateApp/target/ ; cp Spring3HibernateApp.war /var/lib/tomcat8/webapps/ ; sudo service tomcat8 restart"
        }

    }
}
