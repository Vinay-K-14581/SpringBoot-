pipeline {
  agent any
  tools { maven 'Maven 3.9.11' }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
        sh 'pwd; ls -la; echo "--- app/ ---"; ls -la app || true'
      }
    }

    stage('Build') {
      steps {
        echo 'compile maven app'
        dir('app') { sh 'mvn -B -V clean compile' }
        // alt: sh 'mvn -B -V -f app/pom.xml clean compile'
      }
    }

    stage('Test') {
      steps {
        echo 'test maven app'
        dir('app') { sh 'mvn -B test' }
        // alt: sh 'mvn -B -f app/pom.xml test'
      }
    }

    stage('Package') {
      steps {
        echo 'package maven app'
        dir('app') { sh 'mvn -B -DskipTests package' }
        // alt: sh 'mvn -B -DskipTests -f app/pom.xml package'
      }
    }
  }

  post {
    always { echo 'This pipeline is completed..' }
  }
}
