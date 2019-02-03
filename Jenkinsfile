pipeline {
    agent {
        node {
            label 'master'
        }
    }
    parameters {
        booleanParam(name: 'MIRROR REPO SYNC', defaultValue: true, description: 'Toggle this value')
        choice(name: 'DEVICE', choices: ['jfltexx', 'jfvelte'], description: 'Pick something')
        choice(name: 'BRANCH', choices: ['lineage-15.1', 'lineage-16.0'], description: 'Pick something')
    }
    stages {
        stage('Preparation') {
            steps {
                dir("/mnt/los-build/${params.BRANCH}") {
                    sh '''#!/bin/bash
                       set -x\
                       wget https://raw.githubusercontent.com/los-legacy/local_manifests/${params.BRANCH}/${params.DEVICE} -O .repo/local_manifests/${params.DEVICE}
                    '''
                    echo "Device: ${params.DEVICE}"
                    echo "Branch: ${params.BRANCH}"
                }
            }
        }
        stage('Code syncing') {
            steps {
                echo "Device: ${params.DEVICE}"
                echo "Branch: ${params.BRANCH}"
            }
        }        
    }
}
