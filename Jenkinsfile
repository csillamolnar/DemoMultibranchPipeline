node {
  try{
    init()
    checkout()
    build()
    unitTest()
    deploy()
   
  }
  catch (err){

                   mail bcc: '', body: "${err}", cc: '', from: '', replyTo: '', subject: "Failed Pipeline: ${env.JOB_NAME} (${env.BUILD_NUMBER})", to: 'csilla83.molnar@gmail.com'

  }



}
   def init(){
       stage ('Initialize') {

                echo "PATH = ${PATH}"
                 echo "M2_HOME = ${M2_HOME}"
                 echo "${env.JOB_NAME}"
                 echo "${env.BUILD_NUMBER}"
                 echo "${env.BUILD_URL}"
                 echo "${env.JAVA_HOME}"
                 echo "${env.PATH}"

        }
   }
   def checkout(){
        stage 'Checkout code'
        git 'https://github.com/csillamolnar/DemoMultibranchPipeline.git'
   }
   def build(){
        stage 'Build'
        bat 'mvn clean install -Dmaven.test.failure.ignore=true -Dmaven.javadoc.skip=true -Dcheckstyle.skip=true'
   }

   def unitTest() {
    stage 'Unit tests'
    bat 'mvn test -Dmaven.javadoc.skip=true -Dcheckstyle.skip=true'
    if (currentBuild.result == "UNSTABLE") {
        sh "exit 1"
    }
   }
    def deploy(){
        stage 'Deploy'
        bat 'mvn package'

    }




