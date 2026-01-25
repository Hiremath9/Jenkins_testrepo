pipeline{
    agent any
    environment{
        a="Linux"
        part="/"
    }
    stages{
        stage("test"){
            steps{
                 sh("uname")
                 echo "STAGE1 IS COMPLEED"
                 script{
                     def hy=sh(script: 'uname',returnStdout: true).trim()
                     echo "Output os is ${hy}"
                     if ("${hy}" == "${a}"){
                         echo "CORRECT OS"
                         def sgy=sh(script:'sh /tmp/drt.sh ${part}',returnStdout: true).trim()
                         echo "${sgy}"
                         if ("${sgy}" =~ "exceeeded"){
                             echo "There is disk space issue stop the build"
                             error("Build stop due todisk issue")
                         }
                         else{
                             echo "No issue found continue"
                         }
                     }
                     else{
                         echo "WRONG OS"
                         error("Build wil fail since os is not linux")
                     }
                 }
            }
           
        }
        stage("dev"){
            steps{
                sh("free")
                echo "STAGE2 is completed"
            }   
        }
    }
    post{
        always{
            echo "need to chek suucess or failure"
        }
        success{
            echo "build is scucess since all stages completed succesfully"
        }
        failure{
            echo "build is failure"
        }
    }
}
