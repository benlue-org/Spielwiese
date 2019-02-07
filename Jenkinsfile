properties([
  parameters([
    choice(choices: ['jfltexx', 'jfvelte'], description: 'select your device', name: 'DEVICE'), 
    choice(choices: ['15.1', '16.0'], description: 'select your branch', name: 'BRANCH')
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
