LDAP Queries
------------

### Get all DCs

    ldapsearch -x -h <DC IP Address> -b "<Base DN>" -D "<user@fqdn>" -W -s sub "(&(objectCategory=computer)(userAccountControl:1.2.840.113556.1.4.803:=8192))" | grep distinguishedname -i

### Get all user descriptions from AD

    ldapsearch -x -h <DC IP Address> -b "<Base DN>" -D "<user@fqdn>" -W -s sub '(&(objectCategory=person)(objectClass=user))' | grep "cn:\|description:"

### Get all members of Domain Admins group

    ldapsearch -x -h <DC IP Address> -b "<Base DN>" -D "<user@fqdn>" -W -s sub '(&(objectCategory=user)(memberOf=cn=Domain Admins,cn=Users,dc=ad,dc=test,dc=local))' | grep "distinguishedName:"

### Get all machines with “server” in the DN

    ldapsearch -x -h <DC IP Address> -b "<Base DN>" -D "<user@fqdn>" -W -s sub "(objectCategory=computer)" | grep -E "distinguishedname.*server" -i

### Check if you can add a machine to the domain
There are two ways this default functionality can be disabled. First, it can be disabled by changing the default ms-DS-MachineAccountQuota value at the domain to 0 from 10.
#### Check if ms-DS-MachineAccountQuota is &gt; 0

    ldapsearch -x -h <DC IP Address> -b <Base DN>" -D "<user@fqdn>" -W -s sub "(objectclass=domain)" | grep "ms-ds-machineaccountquota" -i

 ### Accounts with SPNs
    
    ldapsearch -x -h <DC IP Address> -b <Base DN>" -D "<user@fqdn>" -W -s sub "(servicePrincipalName=*)"



https://social.technet.microsoft.com/wiki/contents/articles/5392.active-directory-ldap-syntax-filters.aspx
