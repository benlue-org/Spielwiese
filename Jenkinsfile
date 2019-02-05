pipeline {
    agent {
        node {
            label 'master'
        }
    }
    parameters {
        booleanParam(name: 'MIRROR REPO SYNC', defaultValue: true, description: 'Toggle this value')
        booleanParam(name: 'MAKE CLEAN', defaultValue: true, description: 'Toggle this value')
        choice(name: 'DEVICE', choices: ['jfltexx', 'jfvelte'], description: 'Pick something')
        choice(name: 'BRANCH', choices: ['lineage-15.1', 'lineage-16.0'], description: 'Pick something')
    }
    stages {
        stage('Preparation') {
            steps {
                dir("/mnt/los-build/${BRANCH}") {
                    sh '''#!/bin/bash
                       set -x
                       mkdir -p ~/bin
                       curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
                       source ~/.profile
                       make clean
                       rm -rf .repo/local_manifests
                       repo init -u /mnt/los-mirror/LineageOS/android.git -b "$BRANCH"
                       mkdir -p .repo/local_manifests
                       wget https://raw.githubusercontent.com/los-legacy/local_manifests/"$BRANCH"/"$DEVICE".xml -O .repo/local_manifests/"$DEVICE".xml                                        
                    '''
                }
            }
        }
        stage('Repo Sync') {
            steps {
                dir("/mnt/los-build/${BRANCH}") {
                    sh '''#!/bin/bash
                       set -x
                       source ~/.profile
                       repo sync -f --force-sync --force-broken --no-clone-bundle --no-tags -j$(nproc --all)
                       ./device/samsung/jf-common/patches/apply.sh
                    '''
                }
            }
        }
        stage('Build Process') {
            steps {
                dir("/mnt/los-build/${BRANCH}") {
                    sh '''#!/bin/bash
                       set -x
                       source build/envsetup.sh                   
                       breakfast "$DEVICE"
                       export USE_CCACHE=1
                       ccache -M 50G
                       export CCACHE_COMPRESS=1
                       export ANDROID_JACK_VM_ARGS="-Dfile.encoding=UTF-8 -XX:+TieredCompilation -Xmx4G"
                       brunch "$DEVICE"
                       ./device/samsung/jf-common/patches/revert.sh
                    '''
                }
            }
        }        
        stage('Example') {
            steps {
                    echo "Device: ${params.DEVICE}"
                    echo "Branch: ${params.BRANCH}"
            }
        }
    }
}
