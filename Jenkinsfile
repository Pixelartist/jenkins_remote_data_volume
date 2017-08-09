
pipeline {
    agent any
    stages {
        stage('prep') {
            steps {
                sh 'echo Step1 in Prep'
            }
        }
        stage('execute') {
            steps {
            withCredentials([usernamePassword(credentialsId: 'pentaho_root_main', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
            // available as an env variable, but will be masked if you try to print it out any which way
            sh 'echo uname=$USERNAME pwd=$PASSWORD'
            }
                sh 'echo Step outside password'
                sh 'echo $PASSWORD'
            }
        }
    }
}
