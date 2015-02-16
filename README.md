# devenv

Ruby/Rails development environment built with Vagrant and provisioned using Chef. Chef cookbooks are managed using Berkshelf. Fully suited for Ruby/Rails development.

Box is used for developing examples for [How To Cook Microservices](http://howtocookmicroservices.com/).

If you're interested into how this VM was prepared, make sure to review original article [How To Cook Microservices - Development](http://howtocookmicroservices.com/development/)

# Running

    git clone git@github.com:howtocookmicroservices/devenv.git
    cd devenv
    vagrant up
    vagrant provision
    vagrant ssh

## About

### Vagrant plugins
- vagrant-berkshelf: 4.0.2
- vagrant-hostmanager: 1.5.0
- vagrant-omnibus: 1.4.1

### Packages

- Chef Development Kit Version: 0.3.6
- Berkshelf Version: 3.2.3
- To review cookbooks installed in this VM, see **Berksfile**

### Troubleshooting

There's a known issue with CDK and Berkshelf when bringing already provisioned VM up. It raises error like the one below

    stderr: /opt/chefdk/embedded/lib/ruby/2.1.0/fileutils.rb:1402:in `initialize': Permission denied @ rb_sysopen - /Users/*/.berkshelf/vagrant-berkshelf/shelves/berkshelf20141117-36310-1or3u6-default/pelias/.git/objects/02/6d813fd34b114e7deae1eb2c98afed1c1e7f13 (Errno::EACCES)

[How to resolve this problem - vagrant-berkfshelf plugin](https://github.com/berkshelf/vagrant-berkshelf/issues/237#issuecomment-72906999)
