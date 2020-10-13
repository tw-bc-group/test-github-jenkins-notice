void setBuildStatus(String message, String state) {
  step([
      $class: "GitHubCommitStatusSetter",
      reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/tw-bc-group/test-github-jenkins-notice"],
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "ci/jenkins/build-status"],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}

pipeline {
    agent any

    stages {
        stage('test') {

            steps {
                setBuildStatus("Build succeeded", "PENDING");
                echo "Clean fabcar"
            }
        }
    }

    post {
        failure {
            setBuildStatus("Build failed", "FAILURE");
        } 
    }
}

