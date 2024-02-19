---
tags:
  - legacy
  - configuration
---
```plantuml

ConfigurationInitializer -> GamingLogger:getGamingLogger()
activate ConfigurationInitializer
ConfigurationInitializer->Configuration: skinPaths
Configuration->ConfigurationInitializer : Set skinPaths
group while [iterate over skinPaths]
  ConfigurationInitializer -> Configuration: skinPaths.get(skinPath)
  Configuration->ConfigurationInitializer: (TreeSet)skinPathAffIds
  group while [iterate over skinPaths by affiliateId]
    ConfigurationInitializer-> Configuration: getProperty(affId,"ResCacheManager")
    Configuration->ConfigurationInitializer:ResourceCacheManager
    ConfigurationInitializer->ResourceCacheManager:loadResources(servletContext,skinResourcePath)
    activate ResourceCacheManager
    ResourceCacheManager -> ResourceCacheManager: "getResourcePathsFromContext\n(servletContext, contextPath, recursive=true)"
      group for [iterate over resource paths]
        ResourceCacheManager -> ResourceCacheObject: "new ResourceCacheObject\n(resourceName,resourcePath, servletContext)"
        ResourceCacheObject -> ResourceCacheManager: ResourceCacheObject
        
      end
      ResourceCacheManager->ConfigurationInitializer: int (number of resources added \n to the internal resourceMap)
    deactivate ResourceCacheManager
  end
end
deactivate ConfigurationInitializer

```
