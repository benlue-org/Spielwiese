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
                       if [[ ! -e ~/bin/repo ]]; then
                            mkdir -p ~/bin                        
                            curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
                            chmod a+x ~/bin/repo
                       fi
                       set +x
                       source ~/.profile
                       set -x
                       make clean
                       if [[ ! -e .repo/local_manifests/*xml ]]; then
                            rm -rf .repo/local_manifests/*xml
                            wget https://raw.githubusercontent.com/los-legacy/local_manifests/"$BRANCH"/"$DEVICE".xml -O .repo/local_manifests/"$DEVICE".xml
                       fi
                       repo init -u /mnt/los-mirror/LineageOS/android.git -b "$BRANCH"
                    '''
                }
            }
        }
        stage('Repo Sync') {
            steps {
                dir("/mnt/los-build/${BRANCH}") {
                    sh '''#!/bin/bash
                       set +x
                       source ~/.profile
                       set -x
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
                       set +x
                       source build/envsetup.sh
                       set -x
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
        stage('OTA Package') {
            steps {
                dir("/mnt/los-build/${BRANCH}") {
                    sh '''#!/bin/bash
                       set -x
                       echo "some code"
                    '''
                }
            }
        } 
        stage('Archiving') {
            steps {
                dir("/mnt/los-build/${BRANCH}/out/target/product/${DEVICE}") {
                    sh '''#!/bin/bash
                       set -x
                       if [[ ! -e ${BRANCH}-*-UNOFFICIAL-${DEVICE}.zip ]]; then
                            cp ${BRANCH}-*-UNOFFICIAL-${DEVICE}.zip /var/www/html/download/
                            cp ${BRANCH}-*-UNOFFICIAL-${DEVICE}.zip.md5sum /var/www/html/download/
                       fi                       
                    '''
                }
            }
        } 
        stage('Publishing') {
            steps {
                dir("/mnt/los-build/${BRANCH}") {
                    sh '''#!/bin/bash
                       set -x
                       echo "some code"
                    '''
                }
            }
        }          
    }
}
