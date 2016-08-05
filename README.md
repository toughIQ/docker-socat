# docker-socat
Alpine SoCat container for tunneling.

My usecase is to tunnel IPv4 to IPv6 destination. 

Docker host has IPv6 capability, but the containers are kept in the IPv4 realm. If a container has to access an external service, which is only available on IPv6, you can use this container to enable a static IPv4/IPv6 translation.

`docker run -d --net host toughiq/socat`

We use the `--net host` option, since we want to use the IPv6 stack of the host. We avchieve this by binding directly to the host network interface.

To test the setup, just run `curl localhost` on the host which is running the container.

### Default environment settings

	LISTEN_PROTO=TCP4 
	LISTEN_PORT=80 
	TARGET_PROTO=TCP6
	TARGET_HOST=[2a00:1450:400d:803::200e]
	TARGET_PORT=80
  
To override this settings just change your parameter values at runtime. This example changes the listen and target ports to 443:

	docker run -d --net host \
	--env LISTEN_PORT=443 \
	--env TARGET_PORT=443 \
	toughiq/socat
