## Install OpenLDAP

## Pull OpenLDAP
	docker run -d -p 389:389 -v /data/slapd/config:/etc/ldap/slapd.d -v /data/slapd/database:/var/lib/ldap -e LDAP_ORGANISATION=Zerbtech -e LDAP_DOMAIN="idevops.net" -e LDAP_ADMIN_PASSWORD="adc2tek" -e SERVER_NAME="ldap" -e USE_TLS=false --name ldap 192.168.200.3:5000/openldap:0.10.1	
	docker run -p 4403:443 -e LDAP_HOSTS=192.168.200.5 -e SSL_CRT_FILENAME=ldap.crt -e SSL_KEY_FILENAME=ldap.key -v /var/opt/chef-server/nginx/ca:/osixia/phpldapadmin/apache2/ssl -d --name phpldapadmin 192.168.200.3:5000/phpldapadmin:0.5.0	



