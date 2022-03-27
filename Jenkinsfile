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
            stage('Create Tomcat Docker Image') {
                steps {
                    sh "pwd"
                    sh "ls -la"
                    sh "/c/Program\ Files/Docker/Docker/resources/bin/docker build . -t tomcatsamplewebapp:${env.BUILD_ID}"
                }
            }
      }
}