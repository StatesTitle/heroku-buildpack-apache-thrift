# Heroku Buildpack for Apache Thrift compiler

The version of apache thrift on apt-get is very out of date -
it's from 2014 as of this writing (February 2020).

This old version generates invalid python.

This buildpack aims to provide a more up-to-date version of 
the thrift compiler by building the binary from source and
providing this for the app slug.

The thrift binary built ONLY TARGETS Python 3!
