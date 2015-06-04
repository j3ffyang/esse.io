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

## Create User Entry
	cat ldap.ldif 	

	dn: ou=people,dc=esse,dc=io
	ou: people
	description: All developers in organisation
	objectclass: organizationalunit
	
	dn: cn=david,ou=people,dc=esse,dc=io
	objectclass: inetOrgPerson
	cn: james
	displayName: James Bond
	sn: james
	uid: james
	userpassword: mysecret
	homephone: 555-111-2222
	mail: james@esse.io
	description: James Bond
	ou: people

## Load User Entry
Install ldapadd from any box which can access OpenLDAP

	ldapadd -h 192.168.102.2 -x -D "cn=admin,dc=esse,dc=io" -f ldap.ldif -W

## Modify Sample	

	cat ldap_mod.ldif
	dn: ou=people,dc=esse,dc=io
	changetype: Modify
	replace: userpassword
	userpassword: anothersecret
	
	dn: cn=james,ou=people,dc=esse,dc=io
	changetype: Modify
	replace: userpassword
	userpassword: anothersecret

ldapmodify -h 192.168.102.2 -x -D "cn=admin,dc=esse,dc=io" -f ldap_mod.ldif -W

