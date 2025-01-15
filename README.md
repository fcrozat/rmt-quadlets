# Podman quadlet for RMT server

To run a SUSE RMT Server using podman quadlet, just do the following:

* setup your SCC proxy credentials in podman using:

`printf 'your_scc_proxy_username' | podman secret create SCC_USERNAME -`

`printf 'your_scc_proxy_password' | podman secret create SCC_PASSWORD -`

* mkdir -p /srv/rmt
* copy this repository content to /etc/containers/systemd
* copy rmt-server-http.conf to /srv/rmt/vhosts.d
* `systemctl daemon-reload`
* `systemctl start rmt-pod.service`

To run RMT commands, enter the container using:

`podman exec -ti rmt-server /bin/bash`
and run `rmt-cli`.
