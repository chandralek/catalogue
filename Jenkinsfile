pipeline{
  agent{
    label 'SLAVE'
  }

  environment{
    NEXUS_URL=credentials('Nexus')
    MAJOR_VERSION="1.0"
          }
  stages{
    stage('Install Npm dependencies'){
      steps{
        sh '''
      npm install
      '''
      }
    }
    stage('Create archive to upload')
            {
              steps{
                sh '''
              tar -czf catalogue-service-${MAJOR_VERSION}-${BUILD_NUMBER}.tgz node_modules package.json server.js
              '''
              }
            }
    stage('Upload Artifacts to Nexus')
            {
              steps{
                sh '''
          curl -f -v -u $NEXUS --upload-file catalogue-service-${MAJOR_VERSION}-${BUILD_NUMBER}.tgz https://nexus.devopsb46.online/repository/catalogue-service/catalogue-service-${MAJOR_VERSION}-${BUILD_NUMBER}.tgz
              '''
              }
            }
  }
}