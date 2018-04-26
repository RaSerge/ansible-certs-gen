## Description

This playbook intended to generate letsencrypt certs and deploy it (with corresponding nginx domain confs) to "loadbalancer" nodes.

## Requirements
For local env:
1. Installed latest Ansible
2. Installed latest docker
3. Domain registered in route53 (that required letsencrypt certs)
4. Route53 user key/secret with sufficient permissions (see letsencrypt-route53 for more information)
4. The user used in playbook `play` must have ssh (auth by key is strongly recommended) access to "loadbalancer" node with passwordless sudo permissions.

## Arguments (passable variables)
### Required:

  *  `aws_target_domain`=<OUR_AWS_DOMAIN>

### Optional:

  * `generate_ssl_cert`=true/false(default) <define when you want to generate new letsencrypt certificate>
  * `aws_access_key_id`=<AWS_ACCESS_KEY_ID>         #
  * `aws_secret_access_key`=<AWS_SECRET_ACCESS_KEY> # This vars should be defined if you want to generate/renew letsencrypt certificates (when `generate_ssl_cert`/`renew_ssl_cert` is defined)
  * `admin_email`=<YOUR_EMAIL_HERE>"                #
  * `deploy_nginx_conf`=true/false(default) <define when you want to deploy generated nginx conf. By default will be deployed http conf. If `deploy_ssl_cert` is defined also will be deployed https >
  * `deploy_ssl_cert`=true/false(default) <define when you want to deploy generated/renewed letsencrypt certificate>

## USAGE
1. When we want to generate new letsencrypt certificate
```
ansible-playbook -i inventories/testing all.yaml --extra-vars "aws_target_domain=<OUR_AWS_DOMAIN> generate_ssl_cert=true aws_access_key_id=<AWS_ACCESS_KEY_ID> aws_secret_access_key=<AWS_SECRET_ACCESS_KEY> admin_email=<YOUR_EMAIL_HERE> --ask-sudo --private-key=~/.ssh/<YOUR_PRIVATE_KEY>"
```
2. When we want to deploy nginx http configuration
```
ansible-playbook -i inventories/testing all.yaml --extra-vars "aws_target_domain=<OUR_AWS_DOMAIN> deploy_nginx_conf=true --ask-sudo --private-key=~/.ssh/<YOUR_PRIVATE_KEY>"
```
3. When we want to deploy nginx http/https configurations and new/renewed certificates
```
ansible-playbook -i inventories/testing all.yaml --extra-vars "aws_target_domain=<OUR_AWS_DOMAIN> deploy_nginx_conf=true deploy_ssl_cert=true --ask-sudo --private-key=~/.ssh/<YOUR_PRIVATE_KEY>"
```
