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


// pipeline {
//     agent any

//     parameters {
//         choice(
//             name: 'REPOSITORIES', 
//             choices: [
//                     'repo1',
//                     'repo2', 
//                     'repo3'
//                     ],
//             description: 'Select repositories'
//             multiSelect: true)
//         choice(
//             name: 'BRANCHES', 
//             choices: [
//                     'branch1',
//                     'branch2',
//                     'branch3'
//                     ],
//             description: 'Select branches'
//             multiSelect: true)
//     }


//     stages {
//         stage ('Env print') {
//             steps {
//                 script {
//                 sh ```
//                   echo $BRANCHES
//                   echo $REPOSITORIES
//                 ```
//                 }
//             }
//         }
//         stage('Checkout') {
//             steps {
//                 script {
//                     gitBranch = "${params.BRANCHES}".trim()
//                     gitRepo = "${params.REPOSITORIES}".trim()
//                     checkout([$class: 'GitSCM', branches: [[name: gitBranch]], doGenerateSubmoduleConfigurations: false, extensions: [], userRemoteConfigs: [[url: "https://github.com/${gitRepo}.git"]]])
//                 }
//             }
//         }

//         stage('Merge to Master') {
//             echo "Merging ${branch} into ${repo}'s master"
//             when {
//                 expression { params.BRANCHES && params.REPOSITORIES }
//             }
//             steps {
//                 script {
//                     sh "git checkout master"
//                     sh "git merge ${gitBranch}"
//                     sh "git push origin master"
//                 }
//             }
//         }
//     }
// }