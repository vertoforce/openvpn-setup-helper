Info
------

This repo is a docker container that can help run openvpn.

It is run once to set up the openvpn instance on a docker volume, then every other time it is run it uses the config files generated


Configure
------

To configure change server.conf with the desired server config.


Build
-------

To build the docker instance run

`docker built -t openvpn .`


Deploy
------

When deploying, first run the docker instance with the following command:

It will set up the openvpn certificates and ask questions to sign the certificates.  Change the volume name to something you will remember.

`docker run --volume test:/etc/openvpn -ti openvpn /setup_openvpn.sh`


Now whenever running the openvpn container in prod, use the following command:

`docker run -p 1194:1194/udp --privileged --volume test:/etc/openvpn openvpn`


Getting Certs
------

To get certificates out of the volume, run the following command:

`docker volume inspect test`

Then look at the mount point and view the contents there.
