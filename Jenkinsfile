pipeline {
    agent any
    options {
        checkoutToSubdirectory('source')
    }
    
    stages {
        stage ('Build') {
          
            steps {
                dir ('source') {
                    sh '''mvn -Dmaven.test.failure.ignore=true clean deploy
                          cp -R target/*.war ansible/hello-world.war'''
                    artifacts@ nexusArtifactUploader credentialsId: 'd9f4a378-5d45-422a-818f-71790e3bf508', groupId: 'org.reddy    ', nexusUrl: '18.222.122.26:8081/nexus/content/repositories/snapshots/', nexusVersion: 'nexus2', protocol: 'http', repository: 'snapshotRepository', version: '1.0.0-SNAPSHOT'
                    archiveArtifacts '/target/*.war'
                }
                dir ('source/terraform/dev') {
                    sh 'terraform init && terraform apply -auto-approve'
                }
            }
        }
    }
}
