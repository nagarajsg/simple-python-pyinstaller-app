pipeline {
//None parameter in the agent section means that no global agent will be allocated for the entire Pipeline’s
//execution and that each stage directive must specify its own agent section.
    agent any
    stages {
        stage('Build') {
            agent any
            steps {
                //This sh step runs the Python command to compile your application and
                //its calc library into byte code files, which are placed into the sources workspace directory
                sh 'python3 -m py_compile sources/add2vals.py sources/calc.py'
                //This stash step saves the Python source code and compiled byte code files from the sources
                //workspace directory for use in later stages.
                stash(name: 'compiled-results', includes: 'sources/*.py*')
            }
        }
        stage('Test') {
            agent any
            steps {
                //This sh step executes pytest’s py.test command on sources/test_calc.py, which runs a set of
                //unit tests (defined in test_calc.py) on the "calc" library’s add2 function.
                //The --junit-xml test-reports/results.xml option makes py.test generate a JUnit XML report,
                //which is saved to test-reports/results.xml
                
                sh 'python3 -m unittest  sources/test_calc.py'
            }
           
        }
    }
}
