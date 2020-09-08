pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build demo app'
        sh 'sh run_build_script.sh'
      }
    }

    stage('Tests Linux') {
      parallel {
        stage('Tests Linux') {
          steps {
            echo 'Run LInux tests'
            sh 'sh run_linux_tests.sh'
          }
        }

        stage('Tests Windows') {
          steps {
            echo 'RUn Windows tests'
          }
        }

      }
    }

    stage('Deploy staging') {
      steps {
        echo 'Deploy to staging env'
        input 'Ok to deploy'
      }
    }

    stage('Deploy production') {
      steps {
        echo 'Deplot to prod'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'ci-team@example.com', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}