pipeline {
  agent {
    node {
      label 'master'
      /* customWorkspace '/mnt/los-build' */
    }
  }
    environment {
        MIRROR_PATH             = '/mnt/los-mirror/LineageOS/android.git'
        BUILD_PATH              = '/mnt/los-build'
        DEVICE_PATH             = '/mnt/los-build/device'        
        
    	BRANCH                  = 'lineage-15.1'
        DEVICE                  = 'jfltexx'
        
	    USE_CCACHE              =  '1'
        CCACHE_COMPRESS         =  '1'
        ANDROID_JACK_VM_ARGS    =  '-Dfile.encoding=UTF-8 -XX:+TieredCompilation -Xmx4G'
    }
    stages {
        stage('Preparation') {
            steps {
                echo 'Preparation'
                    sh("pwd")
                    sh 'curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo'
                    sh '''#!/bin/bash
                        set -x
                        echo ${'MIRROR_PATH'}
                        echo "Hallo"
                    '''
            }
        }
        stage('OTA Package') {
            steps {
                echo 'OTA Package'
                dir("${BUILD_PATH}") {
                    //sh '''#!/bin/bash\nsource build/envsetup.sh\nbreakfast "${DEVICE}"\nprintenv'''
                }    
            }
        }
        stage('Archiving') {
            steps {
                echo 'Archiving'
                dir("${BUILD_PATH}") {
                    //sh '''#!/bin/bash\nsource build/envsetup.sh\nbreakfast "${DEVICE}"\nprintenv'''
                }    
            }
        } 
        stage('Publishing') {
            steps {
                echo 'Publishing'
                dir("${BUILD_PATH}") {
                    //sh '''#!/bin/bash\nsource build/envsetup.sh\nbreakfast "${DEVICE}"\nprintenv'''
                }    
            }
        }         
    }
}
