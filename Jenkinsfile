pipeline {
  agent none
  stages {
    stage('Build') {
      agent {
        docker {
          image 'python:2.7.16-slim'
          args '--user root'
        }

      }
      steps {
        echo 'Compiling vote app'
        dir(path: 'vote') {
          sh 'pip install -r requirements.txt'
        }

      }
    }

    stage('Unit Test') {
      parallel {
        stage('Unit Test') {
          agent {
            docker {
              image 'python:2.7.16-slim'
              args '--user root'
            }

          }
          steps {
            echo 'Running Unit Tests on vote app'
            dir(path: 'vote') {
              sh 'pip install -r requirements.txt'
              sh 'nosetests -v'
            }

          }
        }

        stage('PS01') {
          agent any
          steps {
            sleep 5
          }
        }

      }
    }

    stage('Docker BnP') {
      agent any
      when {
        branch 'main'
      }
      steps {
        echo 'Packaging vote app with docker'
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
            def voteImage = docker.build("initcron/vote:v${env.BUILD_ID}", "./vote")
            voteImage.push()
            voteImage.push("dev")
            voteImage.push("latest")
          }
        }

      }
    }

    stage('SS02') {
      steps {
        sleep 3
      }
    }

  }
  post {
    always {
      echo 'Pipeline for vote is complete..'
    }

  }
}