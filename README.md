# docker-lab
### A collaborative docker environment

This is a skeleton setup for hosting a docker environment for tmux session sharing. Multiple users can ssh directly into a docker container and share a single tmux session, in isolation from the host computer. All users share the same tmux session, and only the host has access to the root user, through `docker exec -it -u root docker-lab` on the host machine.

The base case is as follows:

1. `git clone https://github.com/1mikegrn/docker-lab.git`
2. `docker-compose up -d`
3. On your home network router (ideally configured with a static ip address), set up port-forwarding such that ssh traffic (port 22, or otherwise) is forwarded to the host machine on your local network, targeting port 2222.

A few benefits to the default setup:
1. docker container is completely isolated from the host
2. Base image is a vanilla archlinux container
3. Guest users are piped directly into tmux
4. Minimal, so highly customizable

## Container access
from the host, access to the user account is: 
- `docker exec -it -u user docker-lab bash`

from the host, access to the root account is: 
- `docker exec -it -u root docker-lab bash`

from a remote location, access to the user account is:
- `ssh user@<HOME_NETWORK_IP_ADDRESS> [-p <PORT>]`

## Final notes:
- The default user/password is `user:password`, this can be changed either in `./src/Dockerfile.docker-lab#L10` or using `passwd` once in the container.
- the user account is tethered to a tmux session on ssh - you can't exit/detach tmux without killing your session. If this is undesired, remove `./src/Dockerfile.docker-lab#L20`
