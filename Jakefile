fs = require('fs');

// ------------------
// SETTINGS
// ------------------

stylusDir = 'src/styl/';
jadeEmailDir = 'src/jade/email/';
jadeSettingsDir = 'src/jade/settings/';
libDir = 'lib/';

// ------------------
// END SETTINGS
// ------------------

function readStylusFiles(stylusDir, callback) {
	var filesArr = [];

	var files = fs.readdirSync(stylusDir, function(err, files) {
		if (err) throw err;
	});

	var nrOfFiles = files.length - 1;

	files.forEach(function(file, i) {

		var stats = fs.statSync(stylusDir + file, function(err) {
			if (err) throw err;
		});

		var fileLower = file.toLowerCase();

		if( stats.isFile() && /^.+(.styl)$/.test(fileLower) ) {
			filesArr.push(file);
		}

		if (i === nrOfFiles) {
			callback(filesArr);
		}

	});
}

function readHtmlFiles(libDir, callback) {
	var filesArr = [];

	var files = fs.readdirSync(libDir, function(err) {
		if (err) throw err;
	});

	var nrOfFiles = files.length - 1;

	files.forEach(function(file, i) {
		var stats = fs.statSync(libDir + file, function(err) {
			if (err) throw err;
		});

		var fileLower = file.toLowerCase();

		if( stats.isFile() && /^.+(.html)$/.test(fileLower) && fileLower.indexOf('-premailed') === -1 ) {
			filesArr.push(file);
		}

		if (i === nrOfFiles) {
			callback(filesArr);
		}

	});
}

function makeTempStylusFiles(files, stylusDir, jadeEmailDir, callback) {
	var nrOfFiles = files.length - 1;
	var tmpFiles = [];

	files.forEach(function(file, i) {

			data = fs.readFileSync(stylusDir + file, 'utf-8', function(err){
				if (err) throw err;
			});

			newdata = ':stylus\n' + data;
			newFileName = file.substr(0, file.lastIndexOf('.'));
			jadeFileName = jadeEmailDir + newFileName + '.jade';
			tmpFiles.push(jadeFileName);

			fs.writeFileSync(jadeFileName, newdata, 'utf-8', function(err) {
				if (err) throw err;
			});

			if (i === nrOfFiles) {
				callback(tmpFiles);
			}
	});
}

function removeTmpStylusFiles(tmpFiles, callback) {
	var nrOfFiles = tmpFiles.length - 1;

	tmpFiles.forEach(function(file, i) {
		fs.unlink(file, function (err) {
			if (err) throw err;
			if (i === nrOfFiles) {
				callback();
			}
		});
	});
}

function compileJade(jadeSettingsDir, libDir, callback) {
	jake.exec('jade --out ' + libDir +  ' --pretty ' +  jadeSettingsDir + '*.jade', function() {
		callback();
	}, { printStdout: false });
}

function runPremailer(libDir, files, callback) {
	var nrOfFiles = files.length - 1;

	files.forEach(function(file, i) {
		newFileName = file.substr(0, file.lastIndexOf('.'));
		jake.exec('premailer -r ' + libDir + file + ' > ' + libDir + newFileName + '-premailed.html', function() {
			if (i === nrOfFiles) {
				callback();
			}
		});
	});
}

desc('Build all source files.');
task('build', function () {

	start = new Date().getTime();

	readStylusFiles(stylusDir, function(stylusFiles) {
		console.log('\nCreating a temp styles file(s)...');
		makeTempStylusFiles(stylusFiles, stylusDir, jadeEmailDir, function(tmpFiles) {
			console.log(' ✓ Completed.');
			console.log('\nCreating HTML file(s) with Jade...');
			compileJade(jadeSettingsDir, libDir, function() {
				console.log(' ✓ Completed.');
				console.log('\nRemoving the temp styles file(s)...');
				removeTmpStylusFiles(tmpFiles, function(){
					console.log(' ✓ Completed.');
					console.log('\nReading HTML file(s)...');
					readHtmlFiles(libDir, function(htmlFiles) {
						console.log(' ✓ Completed.');
						console.log('\nRunning Premailer on HTML file(s)...');
						runPremailer(libDir, htmlFiles, function(){
							console.log(' ✓ Completed.');
							end = new Date().getTime();
							console.log('\nBuiding completed in ' + (end - start) + 'ms\n');
						});
					});
				});
			});
		});
	});

});
