pipeline {
    agent any

    parameters {
        string(defaultValue: "TEST", description: 'What environment?', name: 'userFlag')
        choice(choices: ['jfltexx', 'jfvelte'], description: 'Select build device', name: 'device')
        choice(choices: ['lineage-14.1', 'lineage-15.1', 'lineage-16.0'], description: 'Select build branch', name: 'branch')
    }

    stages {
        stage("test") {
            steps {
                echo "${params.device}"
                echo "${params.branch}"
                echo "flag: ${params.userFlag}"
            }
        }
        stage("preperation") {
            steps {
                echo "Downloading ${params.device}.xml ..."
                echo "repo int -u /mnt/e/los-mirror -b ${params.branch}"
            
            }
        }
        stage("repo sync") {
            steps {
                echo "${params.device}"
                echo "${params.branch}"
                echo "flag: ${params.userFlag}"
            }
        }}
    }
        post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
