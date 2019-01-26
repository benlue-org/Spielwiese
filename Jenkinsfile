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
                sh "echo ${params.device}"
                sh "echo ${params.branch}"
                echo "flag: ${params.userFlag}"
            }
        }
        stage("preperation") {
            steps {
                sh "echo Downloading ${params.device}.xml"
                sh "echo repo int -u /mnt/e/los-mirror -b ${params.branch}"
            
            }
        }
        stage("repo sync") {
            steps {
                sh "echo ${params.device}"
                sh "echo ${params.branch}"
                echo "flag: ${params.userFlag}"
            }
        }
    }
}
