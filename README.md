# MetaResolver_HandleTemplate

# Idea

- The Handle.Net System is used as a central entry point for PID resolution.
- It utilizes the Handle System's "Template Handle" feature
  - s. "HANDLE.NET (Ver. 9) Technical Manual" --> Chapter 11
- A test prefix is prepared for supporting various templates for different ID types.
- Specific handles were created with those templates, which can match on various ID types, each.
- Resolution is offered by
  1. native handle protocol
  2. web proxy with web GUI
  3. REST API
  4. CLI command line (java library + java client)

# Current status

## What works

- Currently, the following ID types are supported

  - ARK
  - arXiv
  - DOI
  - Handle
  - SWHID
  - URN-NBN-DE
  - URN-NBN-FI
  - Zenodo

- The following prefix is used: **21.T11973**
- ~~4 handles are prepared: 1 for ARKs, 1 for arXiv, 1 for SWHID and 1 for URN-NBN-DE, 1 for URN-NBN-FI and 1 for Zenodo ~~~
  - This is now all merged into one handle! (**21.T11973/MR**)
- global proxy resolver to test everything: https://141.5.100.20:8000/
- the global proxy http://hdl.handle.net/ also works
- The landing page of a given pid could be requested if ?landingpage is added at the end of the pid or just only use the pid, for example `21.T11973/MR@urn:nbn:de:hbz:6-85659524771?landingpage` or `21.T11973/MR@urn:nbn:de:hbz:6-85659524771`
- Metadata record as far as offered by the respective providers could be requested if ?metadata is added at the end of the pid, for example `21.T11973/MR@urn:nbn:de:hbz:6-85659524771?metadata`
- Resource of the pid also as far as offered could be requested if ?resource is added at the end of the pid, for example `21.T11973/MR@urn:nbn:de:hbz:6-85659524771?resource`

# Examples

## GUI example

1. Go to https://141.5.100.20:8000/ or https://hdl.handle.net/

2. Put into the text field:
   - **ARK:** `21.T11973/MR@ark:/13030/tf5p30086k`
   - **arXiv:** `21.T11973/MR@arXiv:2302.00338`
   - **SWHID:** `21.T11973/MR@swh:1:cnt:94a9ed024d3859793618152ea559a168bbcbb5e2`
   - **URN-NBN-DE:** `21.T11973/MR@urn:nbn:de:gbv:7-11858/00-1735-0000-002B-7D0C-3-1`
   - **URN-NBN-FI:** `21.T11973/MR@urn:nbn:fi-fe2021080942632`
   - **Zenodo:** `21.T11973/MR@10.5281/zenodo.8056361`
3. Alternatively a pid example and a display type, including landingpage, metadata or resource, could be selected on ~~https://141.5.100.20:8000/ from the given test pids.
4. There is a resolution matrix on ~~https://141.5.100.20:8000/ which indicates the response types available for each given provider.

## Proxy resolver example

- See https://141.5.100.20:8000/

## REST API example

- **ARK:** https://141.5.100.20:8000/api/handles/21.T11973/MR@ark:/13030/tf5p30086k
- **arXiv:** https://141.5.100.20:8000/api/handles/21.T11973/MR@arXiv:2302.00338
- **SWHID:** https://141.5.100.20:8000/api/handles/21.T11973/MR@swh:1:cnt:94a9ed024d3859793618152ea559a168bbcbb5e2
- **URN:NBN:DE** https://141.5.100.20:8000/api/handles/21.T11973/MR@urn:nbn:de:gbv:7-11858/00-1735-0000-002B-7D0C-3-1
- **URN:NBN:FI** https://141.5.100.20:8000/api/handles/21.T11973/MR@urn:nbn:fi-fe2021080942632
