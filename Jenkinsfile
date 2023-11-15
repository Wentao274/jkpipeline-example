// Jenkinsfile
// ----------------------------------------------------------------------
// This is as simple as it gets with declarative pipeline
// ----------------------------------------------------------------------
pipeline {
    agent {
        node {
            label "103_node"
        }
    }
    
    environment {
        STORE_DIR = '/mnt/nvme0n1/jason/jenkins_build/dingostore'
    }
    
    triggers {
        GenericTrigger (
            causeString: 'Generic Cause',
            genericVariables: [
                [key: 'action', value: '$.action'],
                [key: 'merge_commit', value: '$.pull_request.merge_commit_sha'],
                [key: 'author', value: '$.pull_request.user.login'],
                [key: 'repo', value: '$.repository.name'],
                [key: 'ctime', value: '$.pull_request.closed_at']
                ],
            token: '123456',
            regexpFilterText: '$action',
            regexpFilterExpression: '^.*(closed).*$'
            
            )
            
    }

    stages {
        stage('build pre_check') {
            steps {
                echo 'build pre check script'
                sh '''
				${STORE_DIR}/dingo-setup/pipeline_pre_check.sh ${merge_commit} ${author} ${repo} ${ctime}
				'''
            }
        }
    }
}
