@Library('piper-lib-os') _

node {
  deleteDir()
  checkout scm
  setupCommonPipelineEnvironment script: this
  buildExecute script:this
  cloudFoundryDeploy script: this
}
