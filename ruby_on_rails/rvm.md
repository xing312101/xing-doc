# RVM
> reference: https://rvm.io/

## Install
> reference: https://rvm.io/rvm/install

```
$ gpg --keyserver hkp://pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB

$ curl -sSL https://get.rvm.io | bash -s stable

```

## Install Ruby Version
```
$ rvm install youWantRubyVersion
$ rvm use youWantRubyVersion
```

## Setup in porject
```
# method 1
## create .rvmrc
rvm use ruby-version@projectNameOrAnyWord --create
ex: rvm use ruby-1.9.2-head@helloWorld --create

# method 2
## create .ruby-gemset
project_name
ex: helloWorld

## create .ruby-version
ruby-version
ex: ruby-2.3.0
```
