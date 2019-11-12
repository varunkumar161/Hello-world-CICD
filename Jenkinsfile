pipeline {
    agent any
    options {
        checkoutToSubdirectory('source')
    }
    lssss
    stages {
        stage ('Build') {
          
            steps {
                dir ('source') {
                    sh '''mvn -Dmaven.test.failure.ignore=true clean install
                          cp -R target/*.war ansible/hello-world.war'''
                   
                }
                 dir ('source') {
                 archiveArtifacts 'target/*.war'
                     nexusArtifactUploader credentialsId: 'd9f4a378-5d45-422a-818f-71790e3bf508', groupId: 'org.reddy', nexusUrl: '13.59.22.69:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'snapshots', version: '1.0.0-SNAPSHOT'
                 }
                dir ('source/terraform/dev') {
                    sh 'terraform init && terraform apply -auto-approve'
                }
            }
        }
    }
}
