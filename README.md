# ldapauthkeys

By using the AuthorizedKeysCommand configuration options (man sshd_conf), you
can run an arbitrary command to compose the set of public SSH keys allowed for
login for a given username. This allows to look up keys from a LDAP-server or
some other storage. The X.509 certificates can be fetched from AD by a host
running sshd by an ldap query.  The X.509 certificates can then be converted to
a format accepted by sshd for user login. This technique can optionally be
combined with AD integration for user and group managment as outlined in Linux
host with AD-integration. This gives very good scalability and minimal
administration of local users. It also has the advantage of using ssh keys
rather than Kerberos tickets for access over an open Internet.

Configure sshd by setting the AuthorizedKeysCommand-option as described here:

    # sshd_conf config option.  Set the full path, as mandated by sshd.
    # Make sure the /etc/ssh/ldap_password is readable for sshd, e.g. by chown root:
    # touch /etc/ssh/ldap_password
    # chown root.sshd /etc/ssh/ldap_password
    # chmod 640 /etc/ssh/ldap_password
    # echo <the password> > /etc/ssh/ldap_password
    #
    AuthorizedKeysCommand /usr/local/sbin/ldapauthkeys
 
    AuthorizedKeysCommandUser sshd


