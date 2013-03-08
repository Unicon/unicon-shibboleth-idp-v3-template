Unicon Shibboleth Identity Provider Template
==============================

A template for installing the Shibboleth Identity Provider v2.3.8 which uses thr Shib-CAS-Authenticator plugin for external SSO authentication. The shibboleth installer is preconfigured and decorated with additional tasks that would provide a fully functional identity provider ready for deployment. 

#Requirements
- Ensure you have set the `CATALINA_HOME` environment variable
- Ensure you have set the `JAVA_HOME` environment variable
- Ensure you have sufficient permissions to execute the build and deploy artifacts to `$CATALINA_HOME`

#Configuration
The build is controlled by the `install.properties`. Adjust the following settings based on your environment:

```
idp.home=/shibboleth/shibboleth-idp
idp.hostname=shib.server.edu
cas.hostname=sso.server.edu
idp.logging.level=DEBUG
```

## Sample Service Provider
The build is configured to use the test SP service in its metadata. You should be able to test the functionality by registering your Identity Provider metadata with the test SP service. Follow the instructions here.

#Build

* To install the IdP and create the `idp.war` file, execute: `install`
* To install the CAS authenticator bridge, execute: `install bridge`
* To install the IdP web fragment, execute: `install fragment`
* To see a list of targets available, execute: `install -projecthelp`
* If you wish to combine all above tasks into one, simply execute: `install all`

#Run

Simply restart your web container.
