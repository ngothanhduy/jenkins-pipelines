@Library('jenkins-shared-libs') _

pipeline {
    agent any

    options {
        timeout(10)
        timestamps()
        skipDefaultCheckout()
        buildDiscarder logRotator(artifactDaysToKeepStr: '10', artifactNumToKeepStr: '10', daysToKeepStr: '10', numToKeepStr: '10')
    }

    environment {
        ENV1 = "ENV1"
    }

    parameters {
        string(name: 'GIT_URL', defaultValue: '', description: 'Git repo to be cloned.')
        string(name: 'GIT_BRANCH', defaultValue: 'master', description: 'Git branch.')
    }

    stages {
        stage("Checkout") {
            steps {
                script {
                    log.info("Checkout Code")
                    dryStep.initialize()
                    dryStep.checkOut(
                        directory: 'dev',
                        branch: "${params.GIT_BRANCH}",
                        gitUrl: "${params.GIT_URL}"
                    )
                }
            }
        }
    }

    post {
        cleanup {
            cleanWs deleteDirs: true
        }
    }
}