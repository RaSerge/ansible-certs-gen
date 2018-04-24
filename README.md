##USAGE

ansible-playbook -i inventories/local all.yaml --extra-vars "aws_target_domain=<OUR_AWS_DOMAIN> aws_access_key_id=<AWS_ACCESS_KEY_ID> aws_secret_access_key=<AWS_SECRET_ACCESS_KEY> admin_email=<YOUR_EMAIL_HERE>"
