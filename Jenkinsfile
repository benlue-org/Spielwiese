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
        ws('/mnt/los-build/${BRANCH}') {
            echo "Make some preparation"
            echo "init repo in $BUILD_DIR"
            echo "repo init -u $BUILD_DIR/$BRANCH -b $BRANCH"
            pwd()
        }
    }
    stage('Repo Sync') { 
        echo "Syncing repo" 
    }
    stage('Build Process') {
        echo "Start build process"
        echo "Build los rom for $DEVICE with branch $BRANCH"
        echo "in $BUILD_DIR"
    }
    stage('OTA Package') {
        echo "Build OTA Package"
    }
    stage('Archiving') {
        echo "Archiving the build"
    }
    stage('Publishing') {
        echo "Publishing the build"
    }
}
