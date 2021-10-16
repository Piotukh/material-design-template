pipeline {
    agent {
        label slave1
    }
    tools {
        nodejs 'nodejs'
        uglifyjs 'uglify-js@3'
        cleancss 'clean-css-cli@5.1'

    }
    stages {
        parallel('compression') {
            "uglifyjs" : {'uglifyjs /www/css/* -o min'}
            "cleancss" : {'cleancss /www/css/* -o min'}
        }
    }
}
