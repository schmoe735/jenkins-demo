pipeline {
      agent any
      stages {
            stage('Build Application') {
                  steps {
                        sh 'mvn clean package'
                  }
                  post {
                      success {
                          echo "Now archiving Artifacts..."
                          archiveArtifacts artifacts: '**/*.war'

                      }
                  }
            }
            stage('Deploy to staging') {
                steps {
                    build job: 'DeployApplicationStagingEnv'
                }
            }
            stage('Deploy to Production') {
                steps {
                    timeout(time:5, unit: 'DAYS'){
                        input message: 'Approve PRODUCTION Deployment'
                    }
                    build job: 'DeployApplicationProductionEnv'
                }
            }
      }
}