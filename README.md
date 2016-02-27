# le-nginx-site-adder
Script to automatically create a new website with Nginx + Let's encrypt SSL certs. 

You will need to have Nginx pre-installed + let's encrypt. Make sure the binaries of letsencrypt is in: "/opt/letsencrypt/" or change it in the script to your need.

Webroot directory is set to: /var/www/example.com/html

Download the auto-renew script from spiderneo, and the automatically generated certs with my script will auto-renew!

Download the auto-renew script:

sudo curl -L -o /usr/local/sbin/le-renew-webroot https://gist.githubusercontent.com/spiderneo/3f4b66c4282809e228f2/raw/b096655aa8549dc0be7dbaddb25e839e45ed9c35/le-renew-webroot

sudo chmod +x /usr/local/sbin/le-renew-webroot

You can execute it to check the certs:

sudo le-renew-webroot


create the cronjob:

sudo crontab -e

30 2 * * 1 /usr/local/sbin/le-renew-webroot >> /var/log/le-renewal.log

Save and exit. This will create a new cron job that will execute the le-renew-webroot command every Monday at 2:30 am. The output produced by the command will be piped to a log file located at /var/log/le-renewal.log.


IMPORTANT NOTE:

You will need to point the A records of: example.com and www.example.com to your servers IP. If you use Cloudflare then disable to IP masking in order for Let's Encrypt to successfully generate the certs.
