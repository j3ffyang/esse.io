Reference > https://github.com/nickstenning/docker-slapd/blob/master/README.md
      and > [https://github.com/osixia/docker-phpLDAPadmin](https://github.com/osixia/docker-phpLDAPadmin) 

## Pull OpenLDAP

	docker run --name='ldap' -p 389:389 -v /pool/slapd/ldap:/var/lib/ldap \
		-v /pool/slapd/config:/etc/ldap/slapd.d \
		-e LDAP_DOMAIN="esse.io" -e LDAP_ORGANISATION="esse.io" -e LDAP_ADMIN_PASSWORD=mysecret \
		-e SERVER_NAME="ldap" -d nickstenning/slapd

Security Tip: slapd process running over port 389 is open to public if your firewall isn't configured properly!

## Install phpLDAPadmin and Link to OpenLDAP

	docker run --name='phpldapadmin' -p 11443:443 -e LDAP_HOSTS=192.168.102.2 \
		-v /pool/gitlab_ssl/:/osixia/phpldapadmin/apache2/ssl -e SSL_CRT_FILENAME=gitlab.crt \
		-e SSL_KEY_FILENAME=gitlab.key -d osixia/phpldapadmin
