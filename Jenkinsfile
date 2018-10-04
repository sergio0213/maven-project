pipeline {
  agent none
  stages {
    stage('COMPILAR') {
      parallel {
        stage('COMPILAR') {
          agent {
            node {
              label 'Ubuntu'
            }

          }
          steps {
            sh 'mvn clean package'
            archiveArtifacts '**/*.war'
          }
        }
        stage('CheckStyle') {
          steps {
            sh 'mvn checkstyle:checkstyle'
            checkstyle()
          }
        }
      }
    }
    stage('Aprobar') {
      steps {
        input(message: 'quiere desplegar?', ok: 'si')
      }
    }
    stage('Desplegar') {
      agent {
        node {
          label 'Windows'
        }

      }
      steps {
        copyArtifacts(projectName: 'maven-project', flatten: true, fingerprintArtifacts: true)
      }
    }
  }
  environment {
    APACHE_HOME = 'C:\\Tomcat_8.5\\webapps'
  }
}