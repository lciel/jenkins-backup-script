# Jenkins backup script

[![Build Status](https://travis-ci.org/sue445/jenkins-backup-script.svg?branch=master)](https://travis-ci.org/sue445/jenkins-backup-script)

Archive Jenkins settings and plugins

* $JENKINS_HOME/*.xml
* $JENKINS_HOME/plugins/*.jpi
* $JENKINS_HOME/jobs/*/*.xml
* $JENKINS_HOME/users/*

# Usage
```sh
./jenkins-backup.sh /path/to/jenkins_home archive.tar.gz

# add timestamp suffix
./jenkins-backup.sh /path/to/jenkins_home backup_`date +"%Y%m%d%H%M%S"`.tar.gz
```

# run with Jenkins Job
## 1. install Exclusive Execution Plugin
https://wiki.jenkins-ci.org/display/JENKINS/Exclusive+Execution+Plugin

## 2. New Job
![img](http://cdn-ak.f.st-hatena.com/images/fotolife/s/sue445/20131208/20131208001948.png)

## 3. Configure
### Source Code Management > Repository URL
```
https://github.com/sue445/jenkins-backup-script.git
```

* **Recommended** : specify Branch Specifier with latest release tag
* latest tag is `0.0.7`

![0.0.3](http://f.st-hatena.com/images/fotolife/s/sue445/20140331/20140331010645.png)

### Build Triggers > Build periodically
![img](http://cdn-ak.f.st-hatena.com/images/fotolife/s/sue445/20131110/20131110180825.png)

### Build Environment > Set exclusive Execution
![img](http://cdn-ak.f.st-hatena.com/images/fotolife/s/sue445/20131110/20131110194540.png)

### Build > Execute shell
![img](http://cdn-ak.f.st-hatena.com/images/fotolife/s/sue445/20131110/20131110193935.png)

ex.

```bash
./jenkins-backup.sh $JENKINS_HOME /path/to/backup_`date +"%Y%m%d%H%M%S"`.tar.gz
```

# Operability confirmed
* Debian lenny
* CentOS 6

# UnitTest
install ruby 2.1+

```bash
bundle install
bundle exec rake test
```

# Tips
## rotate backup files
```bash
# keep backup with latest 30 days
find /path/to/backup_* -mtime +30 | xargs rm -f
```

# Changelog
## master
[full changelog](https://github.com/sue445/jenkins-backup-script/compare/0.0.7...master)

## 0.0.7
[full changelog](https://github.com/sue445/jenkins-backup-script/compare/0.0.6...0.0.7)

* Get all plugins, cleaner tar file (thx @maafy6)
  * https://github.com/sue445/jenkins-backup-script/pull/14

## 0.0.6
[full changelog](https://github.com/sue445/jenkins-backup-script/compare/0.0.5...0.0.6)

* Minor shell cleanups (thx @SEJeff)
  * https://github.com/sue445/jenkins-backup-script/pull/9
* Escape bug fix and few tweaks (thx @JackLeo)
  * https://github.com/sue445/jenkins-backup-script/pull/11

## 0.0.5
[full changelog](https://github.com/sue445/jenkins-backup-script/compare/0.0.4...0.0.5)

* backup `$JENKINS_HOME/users`
  * https://github.com/sue445/jenkins-backup-script/pull/7

## 0.0.4
[full changelog](https://github.com/sue445/jenkins-backup-script/compare/0.0.3...0.0.4)

* copy failed when job name contains space (thx @rubenjgarcia)
  * https://github.com/sue445/jenkins-backup-script/pull/4

## 0.0.3
[full changelog](https://github.com/sue445/jenkins-backup-script/compare/0.0.2...0.0.3)

* There are cases where the directory is not created

## 0.0.2
[full changelog](https://github.com/sue445/jenkins-backup-script/compare/0.0.1...0.0.2)

* remove archive file if exists

## 0.0.1
* first release
