# docker-dnsmasq

dnsmasq in a docker container, configurable via a [simple web UI](https://github.com/jpillora/webproc)

### Usage

1. Create a [`/opt/dnsmasq.conf`](http://oss.segetech.com/intra/srv/dnsmasq.conf) file on the Docker host

	``` ini
	#dnsmasq config, for a complete example, see:
	#  http://oss.segetech.com/intra/srv/dnsmasq.conf
	#log all dns queries
	log-queries
	#dont use hosts nameservers
	no-resolv
	#use google as default nameservers
	server=8.8.4.4
	server=8.8.8.8
	#serve all .company queries using a specific nameserver
	server=/company/10.0.0.1
	#explicitly define host-ip mappings
	address=/myhost.company/10.0.0.2
	```

2. Run the container

	```
	$ docker run \
		--name dnsmasq \
		-d \
		-p 53:53/udp \
		-p 5380:8080 \
		-v /opt/dnsmasq.conf:/etc/dnsmasq.conf \
		--log-opt "max-size=100m" \
		-e "HTTP_USER=admin" \
		-e "HTTP_PASS=admin" \
		--restart always \
		daocloud.io/sunny5156/docker-dnsmasq
	```


[daocloud]: https://daocloud.io/sunny5156/docker-dnsmasq
