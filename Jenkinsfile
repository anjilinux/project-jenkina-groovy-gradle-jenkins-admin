pipeline {
  agent { label 'gradle' }

  stages {

    stage('Run') {
      steps {
          withCredentials([
              usernamePassword(credentialsId: 'jenkins', usernameVariable: 'JENKINS_USERNAME', passwordVariable: 'JENKINS_TOKEN'),
              usernamePassword(credentialsId: 'newrelic', usernameVariable: 'NEW_RELIC_ACCOUNT_ID', passwordVariable: 'NEW_RELIC_KEY')
          ])
            withGradle {
               sh '''
                gradle \
                  -DJENKINS_USERNAME="$JENKINS_USERNAME" \
                  -DJENKINS_TOKEN="$JENKINS_TOKEN" \
                  -DJENKINS_URL="http://localhost:8080" \
                  -DNEW_RELIC_ACCOUNT_ID="$NEW_RELIC_ACCOUNT_ID" \
                  -DNEW_RELIC_KEY="$NEW_RELIC_KEY" \
                  run --stacktrace
               '''
            }  // withGradle
          } // withCredentials
      } // steps
    } // Run
  }
}