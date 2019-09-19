node {
   environment {
      AZURE_CRED_ID=JenkinsService
      RES_GROUP='javaWebAppResourceGroup'
      WEB_APP='javaWebAppD'
   }
   stage('init') {
      checkout scm
   }
   stage('build') {
      sh '''
         mvn clean package
         cd target
         cp ../src/main/resources/web.config web.config
         cp gs-spring-boot-0.1.0.jar app.jar 
         zip todo.zip app.jar web.config
      '''
   }
   stage('deploy') {
      azureWebAppPublish azureCredentialsId: env.AZURE_CRED_ID,
      resourceGroup: env.RES_GROUP, appName: env.WEB_APP, filePath: "**/todo.zip"
   }
}
