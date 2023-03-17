pipeline {
  agent any
  options {
      buildDiscarder(logRotator(
          // number of builds to keep
          numToKeepStr: env.BRANCH_NAME !=~ /master/ ? '3'
      ))
  }
  stages {
    stage("Define Global Variables") {
      steps {
        println("Done :-)")
      }
    }
  }
}
