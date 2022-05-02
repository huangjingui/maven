#!groovy
String  buildShell = "${env.buildShell}"
pipeline{
   agent  any
   options {
      timestamps()               // 日志会有时间.
      skipDefaultCheckout()            // 删除隐式checkout scm语句
      disableConcurrentBuilds()     // 禁止并行
      timeout(time: 1,unit:'HOURS')  // 流水线超时设置1h
   }
   stages {
      //下载代码
      stage("GetCode"){ //阶段名称
         steps {
            timeout(time:5,unit:"MINUTES"){
               script{ //填写运行代码
                  println('获取代码')
               }
            }
         }
      }
      //构建
      stage("Build"){
         steps{
            timeout(time:20,unit:"MINUTES"){
               script{
                  println('应用打包')
               }
            }
         }
      }
      //代码扫描
      stage("CodeScan"){
         steps{
            timeout(time:30,unit:"MINUTES"){
               script{
                  println('代码扫描')
                  mvnhome = tool "M2"
                  sh "${mvnhome}/bin/mvn ${buildShell}"
               }
            }
         }
      }
   }
   //构建后操作
   post {
      always {
         script {
            println("always")
         }
      }
      success {
         script {
            currentBuild.description += "\n构建成功"
         }
      }
      failure {
         script {
            currentBuild.description += "\n构建失败"
         }
      }
      aborted {
         script {
            currentBuild.description += "\n构建取消"
         }
      }
   }
}
