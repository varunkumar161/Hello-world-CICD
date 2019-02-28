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
                    nexusArtifactUploader artifacts: [[artifactId: 'hello-world', classifier: '', file: './target/*.war', type: '.war']], credentialsId: 'c9a61db1-febc-4dda-9375-0bfef23c3bb7', groupId: 'varun.org', nexusUrl: '13.59.22.69:8081/nexus/content/repositories/snapshots', nexusVersion: 'nexus2', protocol: 'http', repository: 'sanpshot', version: '1.0'
                }
                dir ('source/terraform/dev') {
                    sh 'terraform init && terraform apply -auto-approve'
                }
            }
        }
    }
}
