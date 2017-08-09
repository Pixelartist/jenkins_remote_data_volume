
pipeline {
    agent any
    stages {
        stage('prep') {
            steps {
                sh 'echo Step1 in Prep'
                sh 'ssh -i ~/.ssh/id_rsa root@37.120.174.211 -p 7777  git --git-dir=/opt/telecare/repo/pentaho_test/.git fetch origin && git --git-dir=/opt/telecare/repo/pentaho_test/.git -C /opt/telecare/repo/pentaho_test/ reset --hard origin/master'
            }
        }
        stage('execute') {
            steps {
            withCredentials([usernamePassword(credentialsId: 'pentaho_root_main', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
            // available as an env variable, but will be masked if you try to print it out any which way
            sh '''
              ssh -i ~/.ssh/id_rsa root@37.120.174.211 -p 7777 /opt/pentaho/pan.sh -rep:"Test" -trans:"src2ext/transformation" -level=Minimal -dir:"/"
            '''

            }
                sh 'echo Step outside password'
                sh 'echo $PASSWORD'
            }
        }
    }
}
