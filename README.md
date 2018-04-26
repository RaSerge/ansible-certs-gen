##Description

This playbook intended to generate letsencrypt certs and deploy it (with corresponding nginx domain confs) to "loadbalancer" nodes.

##Requirements
For local env:
1. Installed latest Ansible
2. Installed latest docker
3. Domain registered in route53 (that required letsencrypt certs)
4. Route53 user key/secret with sufficient permissions (see letsencrypt-route53 for more information)
4. The user used in playbook `play` must have ssh (auth by key is strongly recommended) access to "loadbalancer" node with passwordless sudo permissions.

##Arguments (passable variables)
Required:
  aws_target_domain=<OUR_AWS_DOMAIN>

Optional:
  aws_access_key_id=<AWS_ACCESS_KEY_ID>         #
  aws_secret_access_key=<AWS_SECRET_ACCESS_KEY> # This vars should be defined if you want to generate/renew letsencrypt certs/
  admin_email=<YOUR_EMAIL_HERE>"                #



##USAGE

ansible-playbook -i inventories/local all.yaml --extra-vars "aws_target_domain=<OUR_AWS_DOMAIN> aws_access_key_id=<AWS_ACCESS_KEY_ID> aws_secret_access_key=<AWS_SECRET_ACCESS_KEY> admin_email=<YOUR_EMAIL_HERE>"
