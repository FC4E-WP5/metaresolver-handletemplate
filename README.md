# MetaResolver_HandleTemplate

```
<namespace>
    <template delimiter="@">
        <foreach>
            <if value="type" test="equals" expression="URL">
                <if value="extension" test="matches" expression="^(urn:.*)$" parameter="x">
                    <value data="https://nbn-resolving.org/${x[1]}"/>
                </if>
                <else>
                    <if value="extension" test="matches" expression="^(arXiv:.*)$" parameter="x">
                        <value data="https://arxiv.org/abs/${x[1]}"/>
                    </if>
                <else>
                    <if value="extension" test="matches" expression="^(ark:.*)$" parameter="x">
                        <value data="https://n2t.net/${x[1]}"/>
                    </if>
                </if>
                <else>
                <if value="type" test="equals" expression="HS_NAMESPACE">
                </if>
            </else>
        </foreach>
    </template>
</namespace>
```

# Idea

- The Handle.Net System is used as a central entry point for PID resolution
- It utilizes the Handle System's "Template Handle" feature
    - s. "HANDLE.NET (Ver. 9) Technical Manual" --> Chapter 11
- A test prefix is prepared for supporting various templates for different ID types
- Specific handles were created with those templates, which can match on various ID types, each.
- Resolution is offered by
    1. native handle protocol
    2. web proxy with web GUI
    3. REST API
    4. CLI command line (java library + java client)


# Current status

## What works

- Currently, the following ID types are supported
    - URN
    - ARK
    - arXiv
    - Handle
    - DOI
- The following prefix is used (or misused:) ): **21.T11999**
- ~~3 handles are prepared: 1 for URNs, 1 for ARKs, 1 for arXiv~~~
    - This is now all merged into one handle! (**21.T11999/METARESOLVER**)  
- global proxy resolver to test everything: http://vm03.pid.gwdg.de/
- the global proxy http://hdl.handle.net/ also works

### Known issues
- metadata record (handle): the template is not correct yet and rewrites too much. URL works :-)
- only handle-based PIDs metadata record is understood
    - i have no idea how to gather PID metadata from other ID resolvers
- Using vm03.pid.gwdg.de with http works fine. But http**s** will generate a certificate error. You could, however, add "http://vm03.pid.gwdg.de" to your browser valid certificates of security section under browser settings for the certificate to be accepted by your browser (settings - security - show certificates - server - add exception). 


# Examples

## GUI example

1. Go to ~~http://vm03.pid.gwdg.de/~~ http://hdl.handle.net/

2. Put into the text field:
    - **ARK:**   ```21.T11999/METARESOLVER@ark:/13030/tf5p30086k```
    - **arXiv:** ```21.T11999/METARESOLVER@arXiv:2302.00338```
    - **URN:**   ```21.T11999/METARESOLVER@urn:nbn:de:gbv:7-11858/00-1735-0000-002B-7D0C-3-1```


## Proxy resolver example

### ARK

- Resolution:
    - to the object: http://vm03.pid.gwdg.de/21.T11999/METARESOLVER@ark:/13030/tf5p30086k
    - to (Handle) metadata: http://vm03.pid.gwdg.de/21.T11999/METARESOLVER@ark:/13030/tf5p30086k?noredirect

### arXiv

- Resolution:
    - to the object: http://vm03.pid.gwdg.de/21.T11999/METARESOLVER@arXiv:2302.00338
    - to (Handle) metadata: http://vm03.pid.gwdg.de/21.T11999/METARESOLVER@arXiv:2302.00338?noredirect


### URN

- Resolution:
    - to the object: http://vm03.pid.gwdg.de/21.T11999/METARESOLVER@urn:nbn:de:gbv:7-11858/00-1735-0000-002B-7D0C-3-1
    - to (Handle) metadata: http://vm03.pid.gwdg.de/21.T11999/METARESOLVER@urn:nbn:de:gbv:7-11858/00-1735-0000-002B-7D0C-3-1?noredirect



## REST API example

- **ARK:**      http://vm03.pid.gwdg.de/api/handles/21.T11999/METARESOLVER@ark:/13030/tf5p30086k
- **arXiv:**    http://vm03.pid.gwdg.de/api/handles/21.T11999/METARESOLVER@arXiv:2302.00338
- **URN:**      http://vm03.pid.gwdg.de/api/handles/21.T11999/METARESOLVER@urn:nbn:de:gbv:7-11858/00-1735-0000-002B-7D0C-3-1
