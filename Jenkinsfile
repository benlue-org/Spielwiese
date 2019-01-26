pipeline {	
    agent any
    environment {
        MIRROR_PATH     = '/mnt/e/los-mirror/LineageOS/android.git'
        BUILD_PATH      = '/home/lineageos/android/lineage'
        LOCAL_MANIFESTS = '/home/lineageos/android/lineage/.repo/local_manifests'
    }
    parameters {
        /* string(defaultValue: "Android Parametrized build", description: 'What environment?', name: 'userFlag') */
        choice(choices: ['jfltexx', 'jfvelte'], description: 'Select build device', name: 'device')
        choice(choices: ['cm-14.1', 'lineage-15.1', 'lineage-16.0'], description: 'Select build branch', name: 'branch')
        choice(choices: ['local-mirror', 'lineageos-mirror'], description: 'Select sync mirror', name: 'mirror')
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
                sh 'mkdir -p ~/bin'
                sh 'curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo'
                sh 'chmod a+x ~/bin/repo'
                echo "Downloading ${params.device}.xml ..."
            }
        }
        stage("repo sync") {
            steps {
                dir("${BUILD_PATH}") {
                    /* ToDo select mirror */
                    echo "repo init -u ${MIRROR_PATH} -b ${params.branch}"
                    sh '''#!/bin/bash\nset +x\nsource ~/.profile\nrepo sync -f --force-sync --force-broken --no-clone-bundle --no-tags -j$(nproc --all)'''
                echo "Repo was syncing from ${params.mirror}"
                }
            }
        }
        stage("build prozess") {
            steps {
                dir("${BUILD_PATH}") {
                   echo "Building ${params.device} ${params.branch}"
                   sh '''#!/bin/bash\nset +x\nsource ~/.profile\nbrunch jfltexx'''
            
                }
            }
        }
    }
}
