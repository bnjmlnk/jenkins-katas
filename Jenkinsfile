pipeline {
  agent any
  environment { 
        docker_username = 'bnjmlnk'
    }
  stages {
    stage('clone down') {
      agent {
        steps {
          stash exclude '.git', name: 'code'
        }
      }

    stage('Say Hello') {
      parallel {
        stage('Parallel execution') {
          steps {
            sh 'echo "Fuck dig!"'
          }
        }

        stage('build app') {
          agent {
            docker {
              image 'gradle:jdk11'
            }

          options {
            skipDefaultCheckout true
          }

          }
          steps {
            unstash 'code'
            sh 'ci/build-app.sh'
            archiveArtifacts 'app/build/libs/'
            sh "ls"
            deleteDir()
            sh "ls"
          }
        }

          stage('test app') {
            agent {
              docker {
                image 'gradle:jdk11'
              }
          }

      }
    }

  }
}