pipeline {
      agent any
      stages {
        stage('Initialize')
          {
              def dockerHome = tool 'mydocker'
              env.PATH = "${dockerHome}/bin:${env.PATH}"
          }
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
                    sh "docker build . -t tomcatsamplewebapp:${env.BUILD_ID}"
                }
            }
      }
}