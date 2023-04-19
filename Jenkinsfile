pipeline {
  
  environment {
    gitUrl = "https://github.com/powerPlant/masurca-srf.git"
    gitCredential = "github_powerPlant"
    gitBranch = "master"
    appRecipe = "Apptainer"
    appImage = "MaSuRCA"
    appVersion = "4.1.0"
  }

  agent { label 'apptainer' }
  
  stages {
    stage('Clone git') {
      steps {
        git branch: gitBranch, changelog: false, credentialsId: gitCredential, poll: false, url: gitUrl
      }
    }

    stage('Build') {
      steps {
        sh "sudo apptainer build ${appImage}-${appVersion}.sif ${appRecipe}.${appVersion}"
      }
    }

    stage('Copy') {
      steps {
        sh "cp ${appImage}-${appVersion}.sif /workspace/output"
      }
    }
  }
}