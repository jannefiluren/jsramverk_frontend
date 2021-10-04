# jsramverk_frontend

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

### Publish to dbwebb

rsync -av --delete -e "ssh -i $HOME/.ssh/dbwebb.pub" dist/ jamg19@ssh.student.bth.se:www/editor

### Link to site

http://www.student.bth.se/~jamg19/editor/
