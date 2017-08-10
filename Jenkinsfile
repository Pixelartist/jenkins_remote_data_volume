
pipeline {
    agent any
    triggers {
        cron('0 5 * * *')
    }
    options {
        timeout(time: 1, unit: 'HOURS')
    }
    stages {
        stage('prep all jobs') {
            steps {
                sh 'echo Step1 in Prep'
                sh 'ssh -i ~/.ssh/id_rsa root@37.120.174.211 -p 7777 git --git-dir=/opt/telecare/repo/pentaho_test/.git fetch origin'
                sh 'ssh -i ~/.ssh/id_rsa root@37.120.174.211 -p 7777 git --git-dir=/opt/telecare/repo/pentaho_test/.git -C /opt/telecare/repo/pentaho_test/ reset --hard origin/master'
                // adding a demo for mail notifications
                mail bcc: '', body: 'testjenkins', cc: '', from: '', replyTo: '', subject: 'testjenkins', to: 'biothin@gmail.com'
            }
        }
        stage('execute 01') {
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

pipeline {
    agent any
    triggers {
        cron('0 5 * * *')
    }
    options {
        timeout(time: 1, unit: 'HOURS')
    }
    stages {
        stage('prep 02') {
            steps {
                sh 'echo Step1 in Prep'
            }
        }
        stage('execute 02') {
            steps {

              try {
                          sh 'exit 1'
                      }
                      catch (exc) {
                          echo 'Something failed, I should sound the klaxons!'
                          throw
                      }

                sh 'echo Step outside password'
                sh 'echo $PASSWORD'
            }
        }
    }
}
