pipeline {
  agent {
    node {
      label '107_node'
    }

    stages {
        stage('build pre_check') {
            steps {
                echo 'master branch build pre check script'
                sh '''
				${STORE_DIR}/dingo-setup/pipeline_pre_check.sh ${merge_commit} ${author} ${repo} ${ctime}
				'''
      }
    }

  }
  environment {
    STORE_DIR = '/data/dingostore'
  }
  triggers {
    GenericTrigger(causeString: 'Generic Cause', genericVariables: [
                      [key: 'action', value: '$.action'],
                      [key: 'merge_commit', value: '$.pull_request.merge_commit_sha'],
                      [key: 'author', value: '$.pull_request.user.login'],
                      [key: 'repo', value: '$.repository.name'],
                      [key: 'ctime', value: '$.pull_request.closed_at']
                      ], token: '123456', regexpFilterText: '$action', regexpFilterExpression: '^.*(closed).*$')
    }
  }