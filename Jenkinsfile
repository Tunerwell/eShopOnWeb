pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'dotnet build eShopOnWeb.sln'
      }
    }

    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            sh 'dotnet test tests/UnitTests'
          }
        }

        stage('Integration') {
          steps {
            sh 'dotnet test tests/IntegrationTests'
          }
        }

        stage('Functional') {
          steps {
            sh 'dotnet test tests/FunctionalTest'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        sh 'dotnet pusblish eShopOnWeb.sln -o /var/aspnet '
      }
    }

  }
}