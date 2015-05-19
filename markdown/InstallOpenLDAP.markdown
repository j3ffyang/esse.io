Reference > https://github.com/nickstenning/docker-slapd/blob/master/README.md

## Pull OpenLDAP
	mkdir -p /pool/ldap

	docker run -v /pool/ldap:/var/lib/ldap -e LDAP_DOMAIN=esse.io -e LDAP_ORGANISATION="esse.io" \
		-e LDAP_ROOTPASS=mysecret -d nickstenning/slapd




	docker run -d -p 389:389 -v /data/slapd/config:/etc/ldap/slapd.d -v /data/slapd/database:/var/lib/ldap \
		-e LDAP_ORGANISATION=Zerbtech -e LDAP_DOMAIN="idevops.net" -e LDAP_ADMIN_PASSWORD="myseret" -e \
		SERVER_NAME="ldap" -e USE_TLS=false --name ldap 192.168.200.3:5000/openldap:0.10.1	

	docker run -p 4403:443 -e LDAP_HOSTS=192.168.200.5 -e SSL_CRT_FILENAME=ldap.crt -e \
		SSL_KEY_FILENAME=ldap.key -v /var/opt/chef-server/nginx/ca:/osixia/phpldapadmin/apache2/ssl -d \
		--name phpldapadmin 192.168.200.3:5000/phpldapadmin:0.5.0	



