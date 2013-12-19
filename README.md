Shibboleth IdP Installer Template
==============================

A template for installing the [Shibboleth Identity Provider](https://wiki.shibboleth.net/confluence/display/SHIB2/IdPInstall)
which uses the [Shib-CAS-Authenticator plugin](https://github.com/Unicon/shib-cas-authenticator) 
for external SSO authentication. The shibboleth installer is preconfigured and decorated with additional tasks 
that would provide a fully functional identity provider ready for deployment. 

# Versions

```properties
gradleVersion=1.8
shibCasAuthenticatorVersion=1.3.0.1
shibIdpVersion=2.4.0
shibCommonVersion=1.4.0
junitVersion=4.11
servletVersion=2.5
```

# Requirements
- Ensure you have set `$CATALINA_HOME` 
- Ensure you have set `$JAVA_HOME` and `$JAVA_HOME\bin` is in your `$PATH`
- Ensure you have sufficient permissions to execute the build and deploy artifacts to `$CATALINA_HOME`

# Differences
- Idp session lifetime is changed from the default 30 minutes to [1 minute](https://github.com/Unicon/unicon-shibboleth-idp-template/blob/master/installer/2.4.0/src/installer/resources/conf-tmpl/internal.xml#L102)
- External authentication handler is used, delegating SSO to CAS
- Previous session handler is turned off
- Logging levels are changed to be at `DEBUG` by default

# Configuration
The build is controlled by the [`install.properties`](https://github.com/Unicon/unicon-shibboleth-idp-template/blob/master/installer/2.4.0/src/installer/resources/install.properties) file. Adjust the following settings based on your environment:

```properties
cas.hostname=sso.server.edu

idp.hostname=shib.server.edu
idp.home=/opt/shibboleth-idp
idp.status.page.allowedips=127.0.0.1/32 \:\:1/128

# The handler must be explicitly enabled in the configration.
idp.login.ldap.subtreesearch=false
idp.login.ldap.basedn=ou\=people,dc\=example,dc\=org
idp.login.ldap.userfilter=uid\={0}
idp.login.ldap.url=ldap://ldap.example.org
idp.login.ldap.tls=false

idp.logging.level=DEBUG
idp.logging.ldap.level=INFO

# The resolver must be explicitly enabled in the configration. 
idp.attr.resolver.ldap.url=ldap://ldap.example.org
idp.attr.resolver.ldap.basedn=ou=people,dc=example,dc=org
idp.attr.resolver.principal=uid=myservice,ou=system
idp.attr.resolver.principalCredential=myServicePassword
idp.attr.resolver.filter=(uid=$requestContext.principalName)

# InCommon metadata url and cert name
idp.metadata.incommon.url=http://md.incommon.org/InCommon/InCommon-metadata.xml
idp.metadata.incommon.cert=inc-md-cert.pem
```

The  [Shib-CAS-Authenticator plugin](https://github.com/Unicon/shib-cas-authenticator)
may require additional tweaks to the server environment. Additional details are
[posted here]((https://github.com/Unicon/shib-cas-authenticator). This build does not modify the server environment's
configuration at all. The adopter is responsible for making any and all changes needed to the deployment
environment's configuration. (i.e. Tomcat's `server.xml`, etc)

# Testing
* The build is configured to use the test SP service in its metadata. You should be able to test the functionality by [registering your Identity Provider metadata](https://www.testshib.org/metadata.html) with the test SP service. 
* The build is also configured to optionally use a set of trusted partners whose metadata is provided by the configuration file `metadata/TrustedPartners-metadata.xml`
* The build is also configured to accept the [InCommon metadata](https://github.com/Unicon/unicon-shibboleth-idp-template/blob/master/installer/2.4.0/src/installer/resources/conf-tmpl/relying-party.xml#L109). The metadata is expected to be signed and validated by the [metadata siging certificate](https://github.com/Unicon/unicon-shibboleth-idp-template/blob/master/installer/etc/inc-md-cert.pem) file.

# Build
Navigate to the `installer\${shibIdpVersion}\` directory:

* To install the IdP and create the `idp.war` file, execute: `install` (depends on `bridge` too)
* To install the CAS authenticator bridge, execute: `install bridge`
* To install the IdP web fragment, execute: `install fragment`
* If you wish to combine all above tasks into one, simply execute: `install all`
* To see a list of targets available, execute: `install -projecthelp`
