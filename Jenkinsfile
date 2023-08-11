pipeline {
    agent any

    parameters {
        choice(name: 'repositories', choices: 'repo1\nrepo2\nrepo3\nall', description: 'Select repositories to merge')
        choice(name: 'branches', choices: 'branch1\nbranch2\nbranch3\nall', description: 'Select branches to merge')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Merge Branches') {
            when {
                expression {
                    return params.repositories != 'all' && params.branches != 'all'
                }
            }
            steps {
                script {
                    def selectedRepos = readFile('repo--requirements.txt').split('\n')
                    def selectedBranches = readFile('branch--requirements.txt').split('\n')
                    
                    for (repo in selectedRepos) {
                        for (branch in selectedBranches) {
                            echo "Merging ${branch} branch into master in ${repo} repository"
                            // Add your merge logic here
                        }
                    }
                }
            }
        }

        stage('Merge All') {
            when {
                expression {
                    return params.repositories == 'all' && params.branches == 'all'
                }
            }
            steps {
                script {
                    def allRepos = readFile('repo--requirements.txt').split('\n')
                    def allBranches = readFile('branch--requirements.txt').split('\n')
                    
                    for (repo in allRepos) {
                        for (branch in allBranches) {
                            echo "Merging ${branch} branch into master in ${repo} repository"
                            // Add your merge logic here
                        }
                    }
                }
            }
        }
    }
}
