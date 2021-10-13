pipeline {
  agent {label 'mac-sanley'}
  environment {
      revision = ""
  }
  stages {
    stage('Installing') {
        steps {
            echo 'npm install'
            echo 'npm run pod'
        }
    }

    stage('Checking') {
        failFast true
        parallel {
            stage('Styles') {
                steps {
                    echo 'npm run lint'
                }
            }

            stage('Sonar') {
                steps {
                    echo 'Sonar check...'
                }
            }
        }
    }

    stage('Testing') {
        failFast true
        parallel {
            stage('UT') {
                steps {
                    echo 'npm run test'
                }
            }

            stage('E2E-iOS') {
                steps {
                    // sh 'npm run e2e:ios'
                    echo 'npm run e2e:ios'
                }
            }

            stage('E2E-android') {
                steps {
                    // sh 'npm run e2e:android'
                    echo 'npm run e2e:android'
                }
            }
        }
    }

    stage('Deploying') {
        // when {
        //     branch 'master'
        // }

        parallel {
            stage('iOS') {
                stages {
                    stage('dev') {
                        steps {
                            echo 'Build DEV iOS...'
                            echo 'Deploy DEV iOS...'
                        }
                    }

                    stage('QA') {
                        steps {
                            script {
                                input message: 'continue QA?'
                            }
                            echo 'Build QA iOS...'
                            echo 'Deploy QA iOS...'
                        }
                    }

                    stage('UAT') {
                        steps {
                            script {
                                input message: 'continue UAT?'
                            }
                            echo 'Build UAT iOS...'
                            echo 'Deploy UAT iOS...'
                        }
                    }
                } 
            }

            stage('Android') {
                stages {
                    stage('dev') {
                        steps {
                            echo 'Build DEV Android...'
                            echo 'Deploy DEV Android...'
                        }
                    }

                    stage('QA') {
                        steps {
                            script {
                                input message: 'continue QA?'
                            }
                            echo 'Build QA Android...'
                            echo 'Deploy QA Android...'
                        }
                    }

                    stage('UAT') {
                        steps {
                            script {
                                input message: 'continue UAT?'
                            }
                            echo 'Build UAT Android...'
                            echo 'Deploy UAT Android...'
                        }
                    }
                } 
            }
        }
    }
  }
}
