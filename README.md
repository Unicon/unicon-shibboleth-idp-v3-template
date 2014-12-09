Shibboleth IdP Installer Template
==============================

A template for installing the [Shibboleth Identity Provider](https://wiki.shibboleth.net/confluence/display/SHIB2/IdPInstall) which uses the [Shib-CAS-Authenticator plugin][shibcas] for external SSO authentication. The shibboleth installer is preconfigured and decorated with additional tasks that would provide a fully functional identity provider ready for deployment. 

# Features
- A more automated method of installing the Shibboleth Identity Provider.
- CAS `LoginHandler` to delegate to a CAS server for external authentication.
- Built-in configuration support for InCommon metadata.
- Built-in configuration support for TestShib metadata
- Idp session lifetime is changed from the default 30 minutes to [1 minute](https://github.com/Unicon/unicon-shibboleth-idp-template/blob/master/installer/2.4.0/src/installer/resources/conf-tmpl/internal.xml#L102).
- Previous session handler is turned off
- Logging levels are changed to be at `DEBUG` by default
- Externalized configuration for attribute resolution, login handlers, etc.

# Versions

```properties
shibCasAuthenticatorVersion=2.0.4
shibIdpVersion=2.4.3
casClientVersion=3.3.3
```

# Requirements
- Ensure you have set `$CATALINA_HOME` 
- Ensure you have set `$JAVA_HOME` and `$JAVA_HOME\bin` is in your `$PATH`
- Ensure you have sufficient permissions to execute the build and deploy artifacts to `$CATALINA_HOME`

# Configuration

## Installer Settings
The build is controlled by the [`install.properties`](https://github.com/Unicon/unicon-shibboleth-idp-template/blob/master/installer/2.4.0/src/installer/resources/install.properties) file. 

## Shib-CAS Authenticator Settings
The Shib-CAS authenticator's configuration is controlled by an external properties file. Please see [this resource][shib-cas]

The  [Shib-CAS-Authenticator plugin][shibcas] may require additional tweaks to the server environment. Additional details are [posted here][shibcas]. This build does not modify the server environment's configuration at all. The adopter is responsible for making any and all changes needed to the deployment environment's configuration. (i.e. Tomcat's `server.xml`, etc)

# Testing
* The build is configured to use the test SP service in its metadata. You should be able to test the functionality by [registering your Identity Provider metadata](https://www.testshib.org/metadata.html) with the test SP service. 
* The build is also configured to optionally use a set of trusted partners whose metadata is provided by the configuration file `metadata/TrustedPartners-metadata.xml`
* The build is also configured to accept the [InCommon metadata](https://github.com/Unicon/unicon-shibboleth-idp-template/blob/master/installer/2.4.0/src/installer/resources/conf-tmpl/relying-party.xml#L109). The metadata is expected to be signed and validated by the [metadata siging certificate](https://github.com/Unicon/unicon-shibboleth-idp-template/blob/master/installer/etc/inc-md-cert.pem) file.

# Build
Navigate to the `installer\${shibIdpVersion}\` directory:

* To install the IdP and create the `idp.war` file, execute: `install`
* To install the IdP web fragment, execute: `install fragment`
* If you wish to combine all above tasks into one, simply execute: `install all`
* To see a list of targets available, execute: `install -projecthelp`

[shibcas]: https://github.com/Unicon/shib-cas-authn2/
