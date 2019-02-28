pipeline {
    agent any
    options {
        checkoutToSubdirectory('source')
    }
    
    stages {
        stage ('Build') {
          
            steps {
                dir ('source') {
                    sh '''mvn -Dmaven.test.failure.ignore=true clean install
                          cp -R target/*.war ansible/hello-world.war'''
                   
                }
                 dir ('source') {
                 nexusArtifactUploader artifacts: [[artifactId: 'hello-world', classifier: '', file: 'target/hello-world-1.0.0-SNAPSHOT.war', type: 'war']], credentialsId: 'd9f4a378-5d45-422a-818f-71790e3bf508', groupId: 'org.varun', nexusUrl: '13.59.22.69:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'snapshots', version: '1.0'
                 }
                dir ('source/terraform/dev') {
                    sh 'terraform init && terraform apply -auto-approve'
                }
            }
        }
    }
}
