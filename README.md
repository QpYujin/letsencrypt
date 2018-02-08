## Guide to setting letsencrypt/certbot for dns on AWS-EC2-ROUTE53

1. SSH to an ec2 instance, and git clone this repo into it. 
2. Install certbot on instance. First run `wget https://dl.eff.org/certbot-auto` then run `chmod a+x certbot-auto`.
2. Just make one change to default.conf file, on line 8(or close to it), change server_name to a name that you want https to be created for.
3. Run `docker-compose up --build -d`.
4. Get the DNS of the ec2-instance you are on, go to route53, create a new record if domain is not created yet(NOTE: domain name have to be purchased first).
   Assuming domain is already there, enter into domain and create a subdomain, which is the same as your server_name in default.conf. 
5. Once created, set alias on subdomain created, with the dns of ec2-instance, save.
6. Back to ec2-instance, run sudo ./certbot-auto --webroot -w /path/to/location -d {{dns_name}}