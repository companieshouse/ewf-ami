# ami-repository-template
EWF AMI

Basic setup for a EWF AMI using Centos 6.10.

Things this does:

Runs CIS hardening from a community Centos module disabling required areas to support cloud images and some areas we configure later (firewall, logs)

Sets up EPEL (required for some dependancy services)

Configures a basic ClamAV setup - this is a basic setup with minimal configuration to run the service.

Configures the Cloudwatch Agent for remote logging and provides the metrics that will be required for our availability setup

Common elements between EWF and XML:

setenforce 0 - disable selinux for session and make persistent below:
/etc/selinux/config: set SELINUX=permissive
Installed packages from RedHat: 
httpd
openssl
mod_ssl
mod_perl
Installed packages from Oracle: 
oracle-instantclient11.2-basic
oracle-instantclient11.2-devel
oracle-instantclient11.2-sqlplus
 chkconfig  httpd on
groupadd -g600 chlservices
/etc/ld.so.conf: Add following lines then run ldconfig
/usr/lib/oracle/11.2/client64/lib/
/usr/local/lib
TNS Names:
/usr/lib/oracle/11.2/client64/lib/tnsnames.ora
ENV Vars for users of sqlplus:
export LD_LIBRARY_PATH=/usr/lib/oracle/11.2/client64/lib/
export TNS_ADMIN=/usr/lib/oracle/11.2/client64/lib/

EWF Application Specific:
useradd ewflive -g 600
/etc/httpd/modules/mod_cookietrack.so - Not sure where this was built from and looks to be in addition to the standard httpd module set.
/etc/httpd/conf/httpd.conf
/etc/httpd/conf/ewflive_startup.pl
/etc/httpd/conf.d/ewflive_perl.conf
/home/ewflive/ - This is the main application directory
/home/ewflive/config/My/EWFConfig.pm - EWF Application config
Resources needed from existing onsite servers:
/home/ewflive
/usr/local/lib64/perl5 /usr/local/share/perl5 /usr/lib64/perl5/vendor_perl /usr/share/perl5/vendor_perl /usr/lib64/perl5 /usr/share/perl5
/etc/httpd/conf/httpd.conf
Changed Listen Directive to Listen 0.0.0.0:80
/etc/httpd/conf/ewflive_startup.pl
/etc/httpd/conf.d/ewflive_perl.conf



