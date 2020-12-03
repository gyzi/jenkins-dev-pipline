CODE_CHANGES = getGitChanges()
//localhost:8080/env-vars.html
def gv  // define groovy scirpt var
pipline {
    agent any
    enviorment {
        VER = '1.3.1'
        CRED = credentials('jenkin-cred-1')
    }
    parameters {
        string(name: "VERSION", defaultVaule: "" , description: "choose version app to deploy ")
        choice(name: "O.S", choices: ["Windows,Linux"], description: "info to choose win or linux")
        booleanParam(name: "executeTest",defaultValue: true, description: " confirm or deny execute")
    }
    tools {
        maven 'Maven'
        gradle 'Gradle'
    }
    stages {
        
        stage("build") {
            steps {
                // Build steps
                echo " building the app ${VER} "
                // sh "mvn install"
               // npm install
               // npm build
            }  
        }

        stage("Test"){
            steps {
                // Test steps
                when {
                    expression {
                        BRANCH_NAME == 'dev' && CODE_CHANGES == true && param.executeTest == true
                    }
                }
                echo 'Test condintion branch, changes, execute true for the app'
            }
        }

        stage("deploy"){
            steps {
                // Deploy steps
                script {
                    gv = load "script.groovy"
                    gv.deployApp()
                }
               // with Credentials( [ ] )
            }
        }
    }
}
