node{
stage('checkout SCM'){
git branch:'master',url:'https://github.com/Mounesh97/angular-realworld-example-app.git'
}
stage('install node modules'){
bat "npm install"
}
stage('Build'){
bat "npm run ng --build --prod"
}
}
