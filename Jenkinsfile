pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Compilando Proyecto'
        sh ''' gradle clean
                gradle bootJar
           '''
        mail(subject: 'prueba mail', body: 'job failure', to: 'ocadena@sura.com.co', from: 'devops@com')
        emailext(subject: 'correo', body: 'fallo', to: 'ocadena@sura.com.co')
      }
    }
    stage('Test') {
      steps {
        input 'Quiere ejecutar test'
      }
    }
    stage('Test en Paralelo') {
      parallel {
        stage('Test Unitarios') {
          steps {
            sh 'gradle test'
          }
        }
        stage('Test Integarcion') {
          steps {
            echo 'Ejecutando Test Integracion'
          }
        }
      }
    }
    stage('Deploy') {
      steps {
        input 'Desea Desplegar en el Ambiente'
        echo 'Desplegando'
      }
    }
  }
}