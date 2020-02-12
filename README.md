# Heroku Buildpack for Apache Thrift compiler

The version of apache thrift on apt-get is very out of date -
it's from 2014 as of this writing (February 2020).

This old version generates invalid python, so we need the updated version!

This buildpack provides a prebuilt thrift binary for heroku, built on a heroku:16-build docker container.

```
$ docker run -it heroku/heroku:16-build

--- inside the container from here on...
# curl https://codeload.github.com/apache/thrift/tar.gz/v0.13.0 -o thrift.tgz
# tar xfz thrift.tgz
# apt update
# apt install --no-install-recommends -y automake bison curl flex g++ libboost-dev libboost-filesystem-dev libboost-program-options-dev libboost-system-dev libboost-test-dev libevent-dev libssl-dev libtool make pkg-config
# cd thrift-0.13.0
# ./bootstrap.sh
# ./configure --without-as3 --without-cpp --without-qt5 --without-c_glib --without-csharp --without-java  --without-erlang --without-nodejs --without-nodets --without-lua --without-python --without-perl --without-php --without-php_extension  --without-dart --without-ruby --without-haskell --without-go --without-swift --without-rs --without-cl --without-haxe --without-dotnetcore --without-d --prefix=$HOME/vendor
# make
# make install

--- to extract the built thrift binary: 

$ docker ps
$ docker cp % <container id from docker ps>:/root/vendor/bin/thrift ~/downloads/
```

Building thrift compiler from source takes around 5-6 minutes, so compiling from source would not be feasible during deployment.

The thrift binary built ONLY TARGETS Python 3! You can change this by removing some of the options to ./configure above.

The install steps came from the https://hub.docker.com/_/thrift/, but only go up to version 0.12.0. These instructions were updated for the latest version.

