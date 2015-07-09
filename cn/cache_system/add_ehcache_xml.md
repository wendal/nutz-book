# 添加ehcache.xml

Ehcache自带一个默认配置,但我们需要命名这个配置,所以,在conf目录下建一个ehcache.xml
----------------------------------------------------------------------------

```xml
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:noNamespaceSchemaLocation="ehcache.xsd" updateCheck="false"
    monitoring="autodetect" dynamicConfig="true" name="nutzbook">
    <!-- <diskStore path="java.io.tmpdir/shiro-ehcache"/> -->
    <defaultCache
            maxElementsInMemory="10000"
            eternal="false"
            timeToIdleSeconds="120"
            timeToLiveSeconds="120"
            overflowToDisk="false"
            diskPersistent="false"
            diskExpiryThreadIntervalSeconds="120"
            />
    <cache name="shiro-activeSessionCache"
           maxElementsInMemory="10000"
           overflowToDisk="true"
           eternal="true"
           timeToLiveSeconds="0"
           timeToIdleSeconds="0"
           diskPersistent="true"
           diskExpiryThreadIntervalSeconds="600"/>
</ehcache>
```

关键点就是name="nutzbook",因为我们需要让shiro和nutz共享一个ehcache实例.