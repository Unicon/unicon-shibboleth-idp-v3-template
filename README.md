Unicon Shibboleth Identity Provider Template
==============================

A template for installing the [Shibboleth Identity Provider](https://wiki.shibboleth.net/confluence/display/SHIB2/IdPInstall)
which uses the [Shib-CAS-Authenticator plugin](https://github.com/Unicon/shib-cas-authenticator) 
for external SSO authentication. The shibboleth installer is preconfigured and decorated with additional tasks 
that would provide a fully functional identity provider ready for deployment. 

The current version of the Identity Provider used is `2.3.8`.

#Requirements
- Ensure you have set the `CATALINA_HOME` environment variable
- Ensure you have set the `JAVA_HOME` environment variable
- Ensure you have sufficient permissions to execute the build and deploy artifacts to `$CATALINA_HOME`

#Configuration
The build is controlled by the [`install.properties`](https://github.com/Unicon/unicon-shibboleth-idp-template/blob/master/installer/2.3.8/src/installer/resources/install.properties)
. Adjust the following settings based on your environment:

```
idp.home=/shibboleth/shibboleth-idp
idp.hostname=shib.server.edu
cas.hostname=sso.server.edu
idp.logging.level=DEBUG
```

## Sample Service Provider
The build is configured to use the test SP service in its metadata. You should be able to test the 
functionality by [registering your Identity Provider metadata](https://www.testshib.org/metadata.html)
with the test SP service. 

#Build

* To install the IdP and create the `idp.war` file, execute: `install`
* To install the CAS authenticator bridge, execute: `install bridge`
* To install the IdP web fragment, execute: `install fragment`
* If you wish to combine all above tasks into one, simply execute: `install all`
* To see a list of targets available, execute: `install -projecthelp`
