pipeline{
  agent any
  options {
    timestamps()
    buildDiscarder(logRotator(artifactDaysToKeepStr: '5', artifactNumToKeepStr: '10', daysToKeepStr:'5', numToKeepStr: '10'))
    skipDefaultCheckout()
    skipStagesAfterUnstable()
  }
  tools {
    maven 'maven-3.5.0'
    jdk 'jdk_1.8_44'
  }
  stages{
    stage('checkout'){
      steps{
        checkout scm
        script {
          commit_id = checkout(scm).GIT_COMMIT
          echo "Commit id = ${commit_id}"
        }
      }
    }

    stage('build application'){
      steps{
        sh "mvn clean install"
      }
    }
  }
  post{
    always{
        emailext body: 'Jenkins Assignment build # ${BUILD_NUMBER} is ${currentBuild.currentResult}', subject: 'Jenkins Asssignment build # ${BUILD_NUMBER}', to: 'santosh.karla@reancloud.com'
    }

  }
}
