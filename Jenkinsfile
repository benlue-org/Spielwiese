properties([
  parameters([
    choice(choices: ['/mnt/los-mirror'], description: 'select your local mirror dir', name: 'MIRROR_DIR'),
    choice(choices: ['/mnt/los-build'], description: 'select your build dir', name: 'BUILD_DIR'),
    choice(choices: ['jfltexx', 'jfvelte'], description: 'select your device', name: 'DEVICE'), 
    choice(choices: ['lineage-15.1', 'lineage-16.0'], description: 'select your branch', name: 'BRANCH')
  ])
])
node('builder') {  
    stage('Preparation') {
        dir("/mnt/los-build/${BRANCH}") {
            echo "Make some preparation"
            echo "init repo in $BUILD_DIR"
            echo "repo init -u $BUILD_DIR/$BRANCH -b $BRANCH"
            sh '''#!/bin/bash
                if [[ ! -e $BUILD_DIR/$BRANCH/.repo ]]; then
                    repo init -u $MIRROR_DIR/LineageOS/android.git -b $BRANCH
                fi
            '''
            sh '''#!/bin/bash
                if [[ ! -e .repo/local_manifests/*xml ]]; then
                    rm -rf .repo/local_manifests/*xml                         
                fi
            ```
            sh '''#!/bin/bash
                wget https://raw.githubusercontent.com/los-legacy/local_manifests/"$BRANCH"/"$DEVICE".xml -O .repo/local_manifests/"$DEVICE".xml
            '''
            }
    }
    stage('Repo Sync') { 
        dir("/mnt/los-build/${BRANCH}") {
            echo "Make some preparation"
            echo "init repo in $BUILD_DIR"
            echo "repo sync -f --force-sync --force-broken --no-clone-bundle --no-tags -j4"
            sh '''#!/bin/bash
                set -x
                pwd
            '''
        }
    }
    stage('Build Process') {
        dir("/mnt/los-build/${BRANCH}") {
            echo "Starting build process..."
            echo ". build/envsetup.sh"
            echo "lunch lineage_$DEVICE-userdebug"
            echo "make bacon -j4"
            sh '''#!/bin/bash
                set -x
                pwd
            '''
        }
    }
    stage('OTA Package') {
        dir("/mnt/los-build/${BRANCH}") {
            echo "Build OTA package..."
            sh '''#!/bin/bash
                set -x
                pwd
            '''
        }
    }
    stage('Archiving') {
        dir("/mnt/los-build/${BRANCH}") {
            echo "Archiving your build..."
            sh '''#!/bin/bash
                set -x
                pwd
            '''
        }
    }
    stage('Publishing') {
        dir("/mnt/los-build/${BRANCH}") {
            echo "Publishing your build..."
            sh '''#!/bin/bash
                set -x
                pwd
            '''
        }
    }
}
