# Staging module for Puppet

[![Build Status](https://travis-ci.org/voxpupuli/puppet-staging.png?branch=master)](https://travis-ci.org/voxpupuli/puppet-staging)
[![Code Coverage](https://coveralls.io/repos/github/voxpupuli/puppet-staging/badge.svg?branch=master)](https://coveralls.io/github/voxpupuli/puppet-staging)
[![Puppet Forge](https://img.shields.io/puppetforge/v/puppet/staging.svg)](https://forge.puppetlabs.com/puppet/staging)
[![Puppet Forge - downloads](https://img.shields.io/puppetforge/dt/puppet/staging.svg)](https://forge.puppetlabs.com/puppet/staging)
[![Puppet Forge - endorsement](https://img.shields.io/puppetforge/e/puppet/staging.svg)](https://forge.puppetlabs.com/puppet/staging)
[![Puppet Forge - scores](https://img.shields.io/puppetforge/f/puppet/staging.svg)](https://forge.puppetlabs.com/puppet/staging)

Manages staging directory, along with download/extraction of compressed files.

**Use of this module is deprecated.**
New features are unlikely to be added.
Please consider using [puppet-archive](https://github.com/voxpupuli/puppet-archive#migrating-from-puppet-staging)
instead.

## Usage

Specify a different default staging path (must be declared before using resource):

```puppet
class { 'staging':
  path  => '/var/staging',
  owner => 'puppet',
  group => 'puppet',
}
```

Staging files from various sources:

```puppet
staging::file { 'sample':
  source => 'puppet:///modules/staging/sample',
}

staging::file { 'apache-tomcat-6.0.35':
  source => 'http://apache.cs.utah.edu/tomcat/tomcat-6/v6.0.35/bin/apache-tomcat-6.0.35.tar.gz',
}
```

Staging and extracting files:

```puppet
staging::file { 'sample.tar.gz':
  source => 'puppet:///modules/staging/sample.tar.gz'
}

staging::extract { 'sample.tar.gz':
  target  => '/tmp/staging',
  creates => '/tmp/staging/sample',
  require => Staging::File['sample.tar.gz'],
}
```

Deploying a file (combining staging and extract):

```puppet
staging::deploy { 'sample.tar.gz':
  source => 'puppet:///modules/staging/sample.tar.gz',
  target => '/usr/local',
}
```

Staging files currently support the following source:

* http(s)://
* puppet://
* ftp://
* s3:// (requires aws cli to be installed and configured.)
* local (though this doesn't serve any real purpose.)

## Author

Primarily authored by Nan Liu

## Contributors

* Adrien Thebo
* gizero
* Harald Skoglund
* Hunter Haugen
* Justin Clayton
* Owen Jacobson
* Reid Vandewiele
