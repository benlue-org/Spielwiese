properties([
  parameters([
    choice(choices: ['/mnt/los-mirror'], description: 'select your local mirror dir', name: 'MIRROR_DIR'),
    choice(choices: ['/mnt/los-build'], description: 'select your build dir', name: 'BUILD_DIR'),
    choice(choices: ['jfltexx', 'jfvelte'], description: 'select your device', name: 'DEVICE'), 
    choice(choices: ['lineage-15.1', 'lineage-16.0'], description: 'select your branch', name: 'BRANCH')
  ])
])
node('swarm') {  
    stage('Preparation') {
        dir("/mnt/los-build/${BRANCH}") {
            echo "Make some preparation"
            echo "init repo in $BUILD_DIR"
            echo "repo init -u $BUILD_DIR/$BRANCH -b $BRANCH"
            sh ''' set -x
                if [[ ! -e ~/bin/repo ]]; then
                    mkdir -p ~/bin                        
                    curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
                    chmod a+x ~/bin/repo
                fi
            '''
            sh '''
                if [[ ! -e $BUILD_DIR/$BRANCH/.repo ]]; then
                    repo init -u $MIRROR_DIR/LineageOS/android.git -b $BRANCH
                fi
            '''
            sh '''
                if [[ ! -e .repo/local_manifests/*xml ]]; then
                    rm -rf .repo/local_manifests/*xml                         
                fi
                wget https://raw.githubusercontent.com/los-legacy/local_manifests/"$BRANCH"/"$DEVICE".xml -O .repo/local_manifests/"$DEVICE".xml
                git config --global user.name BenJule
                git config --global user.email benlue@s3root.ovh
            '''
            }
    }
    stage('Mirror Sync') { 
            echo "Execute mirror sync..."
            build 'benlue-org/mirror-sync/master'
    }
    stage('Repo Sync') { 
        dir("/mnt/los-build/${BRANCH}") {
            echo "Execute repo sync..."
            build 'benlue-org/mirror-sync/master'
            sh ''' set -x
                source ~/.profile
                repo sync -f --force-sync --force-broken --no-clone-bundle --no-tags -j$(nproc --all)
            '''
        }
    }  
    stage('Patching Process') { 
        dir("/mnt/los-build/${BRANCH}") {
            echo "Execute patch script..."
            sh ''' set -x
                ./device/samsung/jf-common/patches/apply.sh
            '''
        }
    }
    stage('Build Process') {
        dir("/mnt/los-build/${BRANCH}") {
            echo "Starting build process..."
            echo ". build/envsetup.sh"
            echo "lunch lineage_$DEVICE-userdebug"
            echo "make bacon -j4"
            sh ''' set -x
                . build/envsetup.sh
                export USE_CCACHE=1
                ccache -M 50G
                export CCACHE_COMPRESS=1
                export ANDROID_JACK_VM_ARGS="-Dfile.encoding=UTF-8 -XX:+TieredCompilation -Xmx4G"
                lunch lineage_$DEVICE-userdebug
                make bacon -j4
            '''
        }
    }
    stage('Revert Patch') { 
        dir("/mnt/los-build/${BRANCH}") {
            echo "Execute patch script..."
            sh ''' set -x
                ./device/samsung/jf-common/patches/revert.sh
            '''
        }
    }  
    stage('OTA Package') {
        dir("/mnt/los-build/${BRANCH}") {
            echo "Build OTA package..."
            sh ''' set -x
                pwd
            '''
        }
    }
    stage('Archiving') {
        dir("/mnt/los-build/${BRANCH}") {
            echo "Archiving your build..."
            sh ''' set -x
                pwd
            '''
        }
    }
    stage('Publishing') {
        dir("/mnt/los-build/${BRANCH}") {
            echo "Publishing your build..."
            sh ''' set -x
                pwd
            '''
        }
    }
}
