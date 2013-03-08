Welcome to Internet2's Shibboleth

Shibboleth is a federated web authentication and attribute exchange system
based on SAML developed by Internet2 and MACE.

Shibboleth is licensed under the Apache 2.0 license which is provided in the
LICENSE.txt file.

Shibboleth Project Site:
http://shibboleth.internet2.edu/

Shibboleth Documentation Site:
https://wiki.shibboleth.net/confluence/display/SHIB2

Source and binary distributions
http://shibboleth.internet2.edu/downloads

Bug Tracker:
https://bugs.internet2.edu/jira

Upgrading 
====================

from 2.0.0 to 2.1.0
-------------------
The following configuration changes must be made to upgrade from 2.0.0 to 2.1.0
- in internal.xml replace 'org.opensaml.util.storage.MapBasedStorageService' with 
  'edu.internet2.middleware.shibboleth.common.util.EventingMapBasedStorageService'
  as the value for the class attribute of bean 'shibboleth.StorageService' (line 82 in the
  default configuration file)
  
- in service.xml add the service 'shibboleth.StorageService' to the whitespace delimited 
  list of services already present in the service, shibboleth.ServiceServletContextAttributeExporter
  (service definition starts at line 57 in the default configuration file)

- in internal.xml, replace the string 'org.apache.velocity.runtime.resource.loader.StringResourceLoader' 
  with 'edu.internet2.middleware.shibboleth.common.util.StringResourceLoader' (this is located at line 
  41 in the default configuration file)