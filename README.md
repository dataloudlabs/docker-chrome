# docker-chrome

This is a docker container running ubuntu with a minimal X11 server, VNC and Google chrome installed.

### **Be aware of the implications of running this container in an unsecure network, since the VNC service IS NOT really secured!**

This image was based off of [this article on medium](https://medium.com/dot-debug/running-chrome-in-a-docker-container-a55e7f4da4a8)

#### Usage
###### (the most straightforward way)


To run the container simply do

    docker run -it -p 5900:5900 -e VNC_SERVER_PASSWORD=password --user apps --privileged pjsousa/docker-chrome
   
With any VNC Client, you'll be able to connect to the server. For example, if you're on a mac you should be able to use the builtin client with:

    open vnc://<THE CONTAINER IP>:5900

And you're done!


#### Usage
###### (using ssh, but still not 100% failproof)

A possible way of running a container in a remote host could also be using X11 forwarding over ssh.

For that, run the container in the server but map the vnc port only for the remote's localhost

    docker run -it -p 127.0.0.1:5900:5900 -e VNC_SERVER_PASSWORD=<YOURVNCPASSWORD> --user apps --privileged pjsousa/docker-chrome


from yout client host, connect to the remote via ssh with either one of these:

    ssh -L 5902:127.0.0.1:5900 -N <THE REMOTE IP> # this will map the remote :5900 to your client :5902 port
    ssh -L 5902:127.0.0.1:5900 -N -f <THE REMOTE IP> # this will do the same but send the process to the background


Now, in the client host open your vnc connection with

    open vnc://127.0.0.1:5902
    
### **Once again, this is not completelly secure. Even using the X11 forwarding anyone might be temped to fiddle with the vnc connection on the side of your client host**
