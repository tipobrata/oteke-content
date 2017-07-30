+++
title = "Tutorial Gulp dan Less"
date = "2017-07-23T21:49:20+02:00"
tags = ["sass", "gulp", "bower"]
categories = ["frontend"]
author = "tipobrata"
+++

## Buat file `bower.js`
```
{
  "name": "example",
  "private": true,
  "version": "1.0.0",
  "dependencies": {
    "bootstrap": "^3.3.7"
  }
}
```

## Buat file `package.js`

```
{
	"name": "example",
	"private": true,
	"version": "1.0.0",
	"dependencies": {
		"gulp": "^3.9.1",
		"gulp-autoprefixer": "^4.0.0",
		"gulp-cssmin": "^0.2.0",
		"gulp-less": "^3.3.2",
		"gulp-rename": "^1.2.2",
		"gulp-webserver": "^0.9.1"
	}
}
```
## Buat file `bootstrap.less` yang terletak `bootstraps-gulp/source/less/bootstrap.less`

```
@import "../../bower_components/bootstrap/less/bootstrap";
```

## Install Gulp dan bower

```
npm install -g gulp bower
```

## Install plugin gulp ke dalam folder project

```
npm i -S gulp gulp-autoprefixer gulp-less gulp-cssmin gulp-rename gulp-webserver

```

## Install boostraps melalui bower ke dalam folder project

```
bower i -S bootstrap
```

## Buat file `gulpfile.js`

```
const gulp = require('gulp'),
	autoprefixer = require('gulp-autoprefixer'),
	cssmin = require('gulp-cssmin'),
	less = require('gulp-less'),
	rename = require('gulp-rename');
	webserver = require('gulp-webserver');

	/**
	 * @desc Compiles LESS -> CSS
	 */

	gulp.task('css', () => {
		return gulp.src('source/less/bootstrap.less')
			.pipe(less())
			.pipe(autoprefixer({
				browsers: ['last 2 version'],
				cascade: false,
			}))
			.pipe(gulp.dest('wwwroot/css'))
			.pipe(cssmin())
			.pipe(rename({
				suffix: '.min',
			}))
			.pipe(gulp.dest('wwwroot/css'));
	});

	/**
	 * @desc Build assembly all static assets
	 */

	gulp.task('default', ['css', 'fonts', 'js']);

	/**
	 * @desc Copie bootstrap fonts to web root
	 */
	
	gulp.task('fonts', () => {
		return gulp.src('bower_components/bootstrap/fonts/*')
			.pipe(gulp.dest('wwwroot/fonts'));
	});

	/**
	 * @desc Copie bootstrap *.js to web root
	 */
	
	gulp.task('js', () => {
		let src = [
			'bower_components/jquery/dist/jquery*js',
			'bower_components/bootstrap/dist/js/bootstrap*js',
		];
		return gulp.src(src)
			.pipe(gulp.dest('wwwroot/js'));
	});

	/**
	 * @desc Watchers *.less for changes
	 */
	
	gulp.task('watch', () => gulp.watch('source/less/*.less', ['css']));

	/**
	 * @desc Run the webserver
	 */
	
	gulp.task('server', ['default'], () => {
		return gulp.src('wwwroot')
			.pipe(webserver());
	});

```

## pada file `index.html

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- The above 3 meta tags *must* come first in the head; any other head content must come *after* these tags -->
    <title>Bootstrap TEST Template</title>

    <!-- Bootstrap -->
    <link href="css/bootstrap.min.css" rel="stylesheet">

    <!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->
    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/html5shiv/3.7.3/html5shiv.min.js"></script>
      <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
    <![endif]-->
  </head>
  <body>
    <h1>Hello, world!</h1>
    <div class="container">
      <h1>Custom Bootstrap Theme</h1>
        <div class="btn-toolbar">
          <button type="button>" class="btn btn-default" role="button">Default</button>
          <button type="button>" class="btn btn-primary" role="button">Primary</button>
          <button type="button>" class="btn btn-info" role="button">Info</button>
          <button type="button>" class="btn btn-success" role="button">Success</button>
          <button type="button>" class="btn btn-warning" role="button">Warning</button>
          <button type="button>" class="btn btn-danger" role="button">Danger</button>
        </div>
    </div>

    <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
    <script src="js/jquery.min.js"></script>
    <!-- Include all compiled plugins (below), or include individual files as needed -->
    <script src="js/bootstrap.min.js"></script>
  </body>
</html>
```



[Tutorial Gulp](https://webdesign.tutsplus.com/id/tutorials/the-command-line-for-web-design-automation-with-gulp--cms-23642)

[Pilih Warna](https://brandcolors.net/)