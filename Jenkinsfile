pipeline {
 agent any
  stages {
    stage('Clean Workspace'){
      steps {
        cleanWs()
      }
    }
    
    stage('Checkout'){
      steps {
        checkout([$class: 'GitSCM', 
        branches: [[name: '*/master']], 
        doGenerateSubmoduleConfigurations: false, 
        extensions: [], 
        submoduleCfg: [], 
        userRemoteConfigs: [[url: 'https://github.com/devops81/NorthwindTraders.git']]])

      }
    }
    
    stage('dotnet Restore') {
      steps {
        bat label: 'dotnet restore', 
        script: '''
          dotnet restore
          echo "Restore is done Starting Msbuild *************"
        ''' 
      }
    }

    stage('Build') {
      steps {
        script {
          //def msbuild = tool name: 'msbuild_2017', type: 'hudson.plugins.msbuild.MsBuildInstallation'
          tool name: 'msbuild_2017', type: 'msbuild'
          bat "dotnet build"
        }
      }
    }

    stage('UnitTest') {
      steps {
        script {
          bat label: 'Unit Test using Dotnet CLI',
        script: '''
          dotnet test
        '''
        }
      }
    }
	}
	}