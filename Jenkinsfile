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

        stage("Initialize the terraform with module and plugin")
        {
            echo "Initializing the modules and plugin for terraform"
            sh "cd ${params.Environment}_infra; terraform init"
        }

        stage("Plan the infra with terraform")
        {
            echo "Planning the infra for ${params.Environment}"
            sh "cd ${params.Environment}_infra; terraform plan -var region=${Region} -var profile=${Iam_Profile} -var database_password=${Database_Password}"

            mail(to: 'abhishek.dubey@opstree.com',
                subject: "${currentBuild.fullDisplayName} is ready for deployment",
                body: "Please approve the URL for ${params.Environment}: ${env.BUILD_URL}input")

            input message: 'Do you want to deploy terraform code?', submitterParameter: 'Action'
        }


 
    }
}
