pipeline ( 
agent any 
stages ( 
stage('GIT') { 
steps { 
git branch: 'master', 
url: 'https://github.com/AzizHamed8/azizhamed.git' 
} 
} 
stage('compile') { 
steps{ 
sh 'mvn clean compile' 
} 
} 
}
