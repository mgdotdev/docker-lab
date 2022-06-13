# docker-lab
### A collaborative docker environment

This is a skeleton setup for hosting a docker environment for tmux session sharing. Multiple users can ssh directly into a docker container and share a single tmux session, in isolation from the host computer. All users share the same tmux session, and only the host has access to the root user, through `docker exec -it -u root docker-lab` on the host machine.

The base case is as follows:

1. `git clone https://github.com/1mikegrn/docker-lab.git`
2. `docker-compose up -d`
3. On your home network router (ideally configured with a static ip address), set up port-forwarding such that ssh traffic (port 22, or otherwise) is forwarded to the host machine on your local network, targeting port 2222.
4. Users should be able to access the container now from the internet, via `ssh user@<HOME_NETWORK_IP_ADDRESS> [-p <PORT>]`.

A few benefits to the default setup:
1. docker container is completely isolated from the host
2. Base image is a vanilla archlinux container
3. Guest users are piped directly into tmux
4. Minimal, so highly customizable
