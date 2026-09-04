pipeline {
agent any
stages {
stage('Build') {
steps {
sh 'python3 -m venv venv'
sh '. venv/bin/activate && pip install pytest flake8'
}
}
stage('Code Quality') {
steps {
sh '. venv/bin/activate && flake8 cart.py orders.py || true'
}
}
stage('Test') {
steps {
sh '. venv/bin/activate && pytest'
}
}
stage('Package') {
steps {
sh '. venv/bin/activate && python package.py'
archiveArtifacts artifacts: 'foodexpress.zip', fingerprint: true
}
}
}
post {
success {
echo 'SUCCESS: all stages passed and the artifact was created.'
}
failure {
echo 'FAILURE: one stage failed. Open the red stage to see why.'
}
}
}