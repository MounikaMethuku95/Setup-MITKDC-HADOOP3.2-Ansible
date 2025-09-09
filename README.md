Project Setup:

## Role: openldap
Purpose: Provides the directory backend (OpenLDAP) to store Kerberos principals.
- Installs and configures OpenLDAP.
- Sets suffix and rootDN for LDAP.
- Creates base directory tree: People, Groups, Kerberos.
- Adds Kerberos schema to LDAP.
- Creates Kerberos service account for the KDC.

## Role: kerberos
Purpose: Configures MIT KDC with LDAP backend.
- Installs Kerberos server and LDAP plugin.
- Configures krb5.conf, kdc.conf, and kadm5.acl.
- Stashes LDAP bind password.
- Creates Kerberos realm in LDAP.
- Creates admin principal.
- Starts KDC and kadmin services.
- Creates Hadoop service principals and keytabs.

## Role: ssh
Purpose: Integrates SSH with Kerberos (GSSAPI).
- Enables GSSAPIAuthentication in sshd_config.
- Cleans up Kerberos tickets on logout.
- Restarts sshd.

## Role: hadoop
Purpose: Deploys a Kerberized Hadoop 3.1 cluster with systemd integration.
- Installs Java.
- Creates hadoop user and group.
- Downloads and installs Hadoop.
- Creates directories for HDFS storage and keytabs.
- Configures Hadoop XML files (core-site, hdfs-site, yarn-site, mapred-site).
- Formats NameNode (once).
- Deploys systemd service unit files for NameNode, DataNode, ResourceManager, NodeManager, JobHistoryServer.
- Enables and starts all services.
- Provides handlers for restarting Hadoop.

## End-to-End Flow
1. LDAP role sets up directory with Kerberos subtree.
2. Kerberos role configures KDC with LDAP backend and principals.
3. SSH role integrates Kerberos authentication into SSH.
4. Hadoop role configures and secures Hadoop with Kerberos.

Result:
- Central authentication via Kerberos (with LDAP backend).
- Secure SSH logins using Kerberos tickets.
- Secure Hadoop cluster with Kerberos service principals and keytabs.
- All daemons managed via systemd and start on boot.


<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/cba1cb96-5ffb-456e-a249-4cac8182513d" />
