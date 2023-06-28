@Library('piper-lib-os') _

node {
  setupCommonPipelineEnvironment script: this
  buildExecute script:this
  cloudFoundryDeploy script: this
}
