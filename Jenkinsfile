pipeline {
  agent any
  stages{
    stage("Delete images") {
       steps {
            steps {
                sh(returnStdout: true, script: '''#!/bin/bash
                    if [[ "$(docker images -q postgres)" != "" ]]; then
                        docker stop my-postgres
                        docker rm my-postgres
                        docker rmi postgres
                    fi

                    if [[ "$(docker images -q danieldi/backend)" != "" ]]; then
                        docker stop back-end
                        docker rm back-end
                        docker rmi danieldi/backend
                    fi

                    if [[ "$(docker images -q danieldi/front)" != "" ]]; then
                        docker stop font-end
                        docker rm font-end
                        docker rmi danieldi/front
                    fi
                    '''.stripIndent()
                )
            }
       }
    }

    stage('Run images') {
        sh 'docker-compose up'
    }
  }
}