pipeline {
  agent any
  stages {
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

          }
          steps {
            sh 'ci/build-app.sh'
            archiveArtifacts 'app/build/libs/'
            sh "ls"
            deleteDir()
            sh "ls"
          }
        }

      }
    }

  }
}