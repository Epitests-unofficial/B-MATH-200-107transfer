pipeline {
    agent any
    environment {
        PROJECT_NAME = "107 Transfer"
        BINARY_NAME = "107transfer"
        BINARYTEST_REPO = "https://github.com/Epitests-unofficial/BinaryTester.git"
        TEST_REPO = "https://github.com/Epitests-unofficial/B-MATH-200-107transfer.git"
    }
    stages {
        stage ("Building") {
            agent {
                docker {
                    image "epitechcontent/epitest-docker"                    
                }
            }
            steps {
                sh "if test -f Makefile; then make re; fi"
                sh "test -f $BINARY_NAME"
            }
        }
        stage ("Criterion Tests") {
            agent {
                docker { image "epitechcontent/epitest-docker" }
            }
            steps {
                sh "if ! test -f Makefile; then echo 'No Makefile'; exit 0; fi"
                sh "if [ \$(cat Makefile | grep tests_run: | wc -l) = 1 ]; then if make tests_run 2>&1 | grep 'FAIL\\|Error 1'; then exit 1; else exit 0; fi; else: echo 'No Criterion Tests'; fi"
            }
        }
        stage ("BinaryTester Download") {
            steps {
                sh "git clone $BINARYTEST_REPO /tmp/binarytester"
                sh "cd /tmp/binarytester; npm run build"
            }
        }
        stage ("BinaryTester Tests") {
            agent {
                docker { 
                    image "epitechcontent/epitest-docker"
                    args "-v /tmp/binarytester:/tmp/binarytester"
                    }
            }
            steps {
                sh "git clone $TEST_REPO /tmp/tests"
                sh "/tmp/binarytester/bin/cli -s -t 5000 /tmp/tests/test.yaml"
            }
        }
    }

    post {
        always {
            emailext subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!',
            body: '${SCRIPT, template="groovy-html.template"}',
            recipientProviders: [buildUser(), contributor(), developers(), requestor()],
            attachLog: true,
            from: 'autotest@mail.jenkins.nicojqn.fr'
        }
    }
}
