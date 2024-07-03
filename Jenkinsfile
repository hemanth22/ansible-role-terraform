// Jenkinsfile

@library('ansibleUtils') _

pipeline {
  agent any
  stages {
    stage('Downloading code') {
      steps {
        git(
          branch: 'main',
          url: 'https://github.com/hemanth22/ansible-role-terraform'
        )
      }
    }
    stage('ansible-lint test') {
      steps {
        def errors = ansibleLint('ansible-lint .')
        echo "Ansible Lint Errors: ${errors.join("\n")}"
      }
    }
    stage('Check build status') {
      steps {
        wget(
          url: 'https://gistcdn.githack.com/hemanth22/c92ffc14a478abe004dee2d1b3e317c7/raw/dad16f61248886488b6e6e1a40cb1d6b5649cd03/GPT3.py',
          output: 'GPT3.py'
        )
        python3(
          script: 'GPT3.py'
        )
        appendText(
          text: '## Possible solution by ChatGPT on Circle CI Build Error',
          file: 'ansible_lint_error.txt'
        )
        appendText(
          text: readFile('possible_solutions.txt'),
          file: 'ansible_lint_error.txt'
        )
      }
    }
    stage('Archive') {
      steps {
        archiveArtifacts(
          artifacts: '*'
        )
      }
    }
  }
}
