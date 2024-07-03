pipeline{
      agent any
      stages {
          stage('Downloading code') {
          steps{
          git branch: 'main', url: 'https://github.com/hemanth22/ansible-role-terraform'
          }
          }// Downloading
          stage('ansible-lint test') {
          steps {
          sh 'ansible-lint . | tee >> ansible_lint_error.txt'
          }
          } //Compile
          stage('Check build status') {
          steps {
          sh 'wget -O GPT3.py https://gistcdn.githack.com/hemanth22/c92ffc14a478abe004dee2d1b3e317c7/raw/dad16f61248886488b6e6e1a40cb1d6b5649cd03/GPT3.py'
          sh 'python3 GPT3.py'
          sh 'echo "## Possible solution by ChatGPT on Circle CI Build Error" >> ansible_lint_error.txt'
          sh 'cat possible_solutions.txt >> ansible_lint_error.txt'
          sh 'wget -O create_github_issue.py https://gist.github.com/hemanth22/b1f8ad052685e106820e5d771b58034f/raw'
          sh 'python3 create_github_issue.py'
          }
          } // Execute
          stage ('Archive') {
          steps {
          archiveArtifacts '*'
          }
          } // Archive
      } // stages
} //pipeline
