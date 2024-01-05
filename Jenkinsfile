      pipeline {
          agent any
          tools {
              maven "MAVEN3"
              jdk "OracleJDK8"
          }

    environment {
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'zFaR6wiX8E434p'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpro-maven-central'
        NEXUSIP = '10.0.0.11'
        NEXUSPORT = '8081'
        NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
    }


          stages {
              stage('Build'){
                  steps {
                      sh 'mvn -s settings.xml -DskipTests install'
                  }
                  post {
                      success {
                          echo "Now Archiving."
                          archiveArtifacts artifacts: '**/*.war'
                      }
                  }
              }

              stage('Test'){
                  steps {
                      sh 'mvn -s settings.xml test'
                  }

              }

              stage('Checkstyle Analysis'){
                  steps {
                      sh 'mvn -s settings.xml checkstyle:checkstyle'
                  }
              }
          }
      }
