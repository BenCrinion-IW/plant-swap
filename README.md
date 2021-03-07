# Expo React Native

## Summary

This is a VSCode devcontiner with a bootstrapped  react native/expo application using the "minimalist Typescript" template.

## Running Expo

In order to use the expo mobile app when using the docker container you need an environment variable with the public IP of the docker host. The IP needs to be reachable by the phone (i.e. probably be on the same network unless you've somehow got a public IP address).

``` bash
cd AwesomeProject
export REACT_NATIVE_PACKAGER_HOSTNAME="192.168.1.xx"
expo start
```