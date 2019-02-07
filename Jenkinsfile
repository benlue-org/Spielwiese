properties([
  parameters([
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
