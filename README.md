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
- Ensure you have set `$ANT_HOME` and `$ANT_HOME\bin` is in your `$PATH`
- Ensure you have sufficient permissions to execute the build and deploy artifacts to `$CATALINA_HOME`

# Configuration
The build is controlled by the [`install.properties`](https://github.com/Unicon/unicon-shibboleth-idp-template/blob/master/installer/2.4.0/src/installer/resources/install.properties) file. Adjust the following settings based on your environment:

```properties
idp.home=/shibboleth/shibboleth-idp
idp.hostname=shib.server.edu
cas.hostname=sso.server.edu
idp.logging.level=DEBUG
```

The  [Shib-CAS-Authenticator plugin](https://github.com/Unicon/shib-cas-authenticator)
may require additional tweaks to the server environment. Additional details are
[posted here]((https://github.com/Unicon/shib-cas-authenticator)


# Testing
* The build is configured to use the test SP service in its metadata. You should be able to test the functionality by [registering your Identity Provider metadata](https://www.testshib.org/metadata.html) with the test SP service. 
* The build is also configured to optionally use a set of trusted partners whose metadata is provided by the configuration file `metadata/TrustedPartners-metadata.xml`
* The build is also configured to accept the [InCommon metadata](http://wayf.incommonfederation.org/InCommon/InCommon-metadata.xml). The metadata is expected to be signed and validated by the `incommon.pem` file that the build locally keeps track of at `credentials/incommon.pem`.

# Build
Navigate to the `installer\${shibIdpVersion}\` directory:

* To install the IdP and create the `idp.war` file, execute: `install` (depends on `bridge` too)
* To install the CAS authenticator bridge, execute: `install bridge`
* To install the IdP web fragment, execute: `install fragment`
* If you wish to combine all above tasks into one, simply execute: `install all`
* To see a list of targets available, execute: `install -projecthelp`
