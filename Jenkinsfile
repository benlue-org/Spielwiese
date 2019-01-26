pipeline {
    agent any

    parameters {
        string(defaultValue: "TEST", description: 'What environment?', name: 'userFlag')
        choice(choices: ['jfltexx', 'jfvelte'], description: 'Select build device', name: 'device')
        choice(choices: ['lineage-14.1', 'lineage-15.1', 'lineage-16.0'], description: 'Select build branch', name: 'branch')
    }

    stages {
        stage("foo") {
            steps {
                sh "echo ${params.device}"
                sh "echo ${params.branch}"
                echo "flag: ${params.userFlag}"
            }
        }
    }
}
