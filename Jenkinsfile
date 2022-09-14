#!/usr/bin/env groovy
@Library(['piper-lib@1.171.0', 'piper-lib-os@v1.223.0']) _

def githubWDFCredentialId = 'GITHUB_TOKEN'

// The target configuration file to be used as a front-runner for deployment, back-end switch and integration tests.
def frontRunnerTarget = 'external.production.cfjp10.yaml'

library identifier: 'piper-customDefaultConfiguration@v0.9.2', retriever: modernSCM(
  [$class: 'GitSCMSource', remote: 'https://github.wdf.sap.corp/ConCISe/piper-customDefaultConfiguration.git', credentialsId : githubWDFCredentialId])
library identifier: 'steward-pipeline-utils@v0.16.10', retriever: modernSCM(
  [$class: 'GitSCMSource', remote: 'https://github.wdf.sap.corp/steward-ci/steward-pipeline-utils.git', credentialsId: githubWDFCredentialId])
pipeline {
  agent any
  options {
      timestamps()
      disableConcurrentBuilds()
  }
  stages {
    stage("Define Global Variables") {
        steps {
            script {
                PROMOTEINFO = readJSON file: "${env.WORKSPACE}/xmake_promote.json"
                VERSION = "${PROMOTEINFO.'base.version'}-release-${env.GIT_COMMIT}"
                echo "Promote Info: ${PROMOTEINFO}"
            }
        }
    }
    stage("Download MTAR File and Verify its Signature") {
        when {
            branch 'master'
        }        
        steps {
            script {
              downloadMtarFile(script: this, promoteInfo: PROMOTEINFO)
              verifyMtarFileSignature(promoteInfo: PROMOTEINFO)
            }
        }
    }
  }
}
