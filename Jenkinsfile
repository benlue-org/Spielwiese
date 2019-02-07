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
        echo "repo ini -u url -b $BRANCH" 
    }
    stage('Repo Sync') { 
        echo "Syncing repo" 
    }
    stage('Build Process') { 
        echo "Build los rom for $DEVICE with branch $BRANCH" 
    }
    stage('OTA Package') {
        //
    }
    stage('Archiving') {
        //
    }
    stage('Publishing') {
        //
    }
}
