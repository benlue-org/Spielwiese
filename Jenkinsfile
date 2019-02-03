node {
    stage('Example1') {
        if (env.BRANCH_NAME == 'master') {
            echo 'I only execute on the master branch'
        } else {
            echo 'I execute elsewhere'
        }
    }
    stage('Example2') {
        if (env.BRANCH_NAME == 'device_build') {
            echo 'I only execute on the master branch'
        } else {
            echo 'I execute elsewhere'
        }
    }    
}
