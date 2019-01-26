pipeline {	
    agent any
    parameters {
        string(defaultValue: "Android Parametrized build", description: 'What environment?', name: 'userFlag')
        choice(choices: ['jfltexx', 'jfvelte'], description: 'Select build device', name: 'device')
        choice(choices: ['lineage-14.1', 'lineage-15.1', 'lineage-16.0'], description: 'Select build branch', name: 'branch')
        choice(choices: ['local-mirror', 'lineageos-mirror'], description: 'Select sync mirror', name: 'repo-mirror')
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
        }
    }
}
