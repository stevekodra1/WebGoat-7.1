pipeline {
    agent any
    tools {
        maven 'Maven 3.3.9'
    }
    stages {
        /*
        stage ('Initialize') {
            steps {
                sh 'echo === init stage ==='
                // e.g. "M2_HOME = ${M2_HOME}"
            }
        }

        stage ('Build') {
            steps {
                sh 'echo === build stage ==='
                sh 'cd old_depproject; mvn -Dmaven.test.failure.ignore=true install'
            }
        }

        stage ('Test') {
            steps {
                sh 'echo === test stage ==='
            }
        }
        */

        stage ('Dependency Check') {
            steps {
                sh 'echo === security stage ==='
                sh 'echo === OWASP dependency check ==='
                sh 'cd old_depproject; mvn clean dependency:copy-dependencies'
                sh 'cd old_depproject; ./aggregatefordepcheck.sh'
                dependencyCheckAnalyzer scanpath: 'old_depproject', \
                  outdir: 'depcheck/report', \
                  datadir: '/var/jenkins_home/depcheck/nvdupdates', \
                  hintsFile: '', \
                  includeVulnReports: true, \
                  includeCsvReports: true, \
                  includeHtmlReports: true, \
                  includeJsonReports: true, \
                  isAutoupdateDisabled: true, \
                  skipOnScmChange: false, \
                  skipOnUpstreamChange: false, \
                  suppressionFile: '', \
                  zipExtensions: ''

               dependencyCheckPublisher pattern: 'depchec/report/dependency-check-report.xml', \
                  failedTotalAll: '0', \
                  usePreviousBuildAsReference: false
            }
        }
    }
}
