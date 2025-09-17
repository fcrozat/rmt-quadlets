# Podman quadlets for RMT server

To run a SUSE RMT Server using podman quadlets, just do the following:

* setup your SCC proxy credentials in podman using:

`printf 'your_scc_proxy_username' | podman secret create SCC_USERNAME -`

`printf 'your_scc_proxy_password' | podman secret create SCC_PASSWORD -`

* `mkdir -p /srv/rmt/{ssl,vhosts.d}`
* copy this repository content to `/etc/containers/systemd`
* copy `rmt-server-http.conf` to `/srv/rmt/vhosts.d`
* Optionally generate self-signed certificate with:
    + `openssl req -new -nodes -newkey rsa:2048 -keyout rmt-server.key -out rmt-server.csr -config rmt_server_generation.cnf`
    + `openssl x509 -req -days 365 -in rmt-server.csr -signkey rmt-server.key -out rmt-server.crt -extensions v3_req -extfile rmt_server_generation.cnf`
* Copy SSL certificate to `/srv/rmt/ssl` 
* `systemctl daemon-reload`
* `systemctl start rmt-pod.service`

To run RMT commands, enter the container using:

`podman exec -ti rmt-server /bin/bash`
and run `rmt-cli`.
