# OTUS_Homework_11
 
Project creates one YC LB, 2 nginx proxy server + salt minions, 2 nginx+php-fpm+wordpress backends, pxc cluster+proxysql(3 servers) and salt master.\
### Project Scheme
![Project Scheme](https://github.com/makkorostelev/OTUS_Homework_11/blob/main/Screenshots/scheme.png)\


### Prerequisite

- **Ansible 2.9+**

To work with the project you need to write your data into variables.tf.\
![Variables](https://github.com/makkorostelev/OTUS_Homework_11/blob/main/Screenshots/variables.png)\
Then enter the commands:
`terraform init`\
`terraform apply`

After ~5 minutes project will be initialized and run:\
Below there is an example of successful set up:

```
Outputs:

admin_ip = "51.250.46.192"
backend_ips = [
  "10.5.0.4",
  "10.5.0.30",
]
database_ips = [
  "10.5.0.24",
  "10.5.0.18",
  "10.5.0.25",
]
kafka_ip = "10.5.0.10"
lb_ip = "51.250.45.200"
nginx_ips = [
  "10.5.0.14",
  "10.5.0.20",
]
opensearch_dashboard_ip = "51.250.43.49"
opensearch_ips = [
  "10.5.0.28",
  "10.5.0.23",
  "10.5.0.35",
]

```

You can access salt-master through admin bastion host.
To login enter the command below:\
`ssh ubuntu@admin_ip`\
`ssh salt`

You need to wait for ~5 minutes till minions are ready to accept connections.
Then you can test, if they are ready:
`sudo salt '*' test.ping`

If they are ready, you can apply nginx and iptables states by commands below:\
`sudo salt '*' state.apply nginx`\
`sudo salt '*' state.apply iptables`