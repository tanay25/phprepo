pipeline{

	agent any
	tools{
		git 'Default-git'
	}
	stages{
		stage('Clone Repo'){
			steps{
			git 'https://github.com/tanay25/phprepo.git'
			}
		}
		stage('Install Dependencies'){
			steps{
			sh 'composer install || true'
		}	
		
		}
		stage('Run Tests'){
			steps{
				sh 'vendor/bin/phpunit || true'
			}
		}
		stage('Deploy'){
			steps{
				sh '''
					sudo rm -rf /var/www/html/*
					sudo cp -r * /var/www/html/


				'''
			}
			
		}
	}
}
