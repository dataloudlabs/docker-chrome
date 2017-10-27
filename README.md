# docker-chrome

This is a docker container running ubuntu with a minimal X11 server, VNC and Google chrome installed.

**Be aware of the implications of running this container in an unsecure network, since the VNC service IS NOT inherently secured!**

This image was based off of [this article on medium](https://medium.com/dot-debug/running-chrome-in-a-docker-container-a55e7f4da4a8)

To run the container simply do

    docker run -it -p 5900:5900 -e VNC_SERVER_PASSWORD=password --user apps --privileged pjsousa/docker-chrome
   
With any VNC Client, you'll be able to connect to the server. For example, if you're on a mac you should be able to use the builtin client with:

    open vnc://<THE CONTAINER IP>:5900

