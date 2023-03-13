---
title: Getting started
layout: home
nav_order: 1
---

# Getting started

FIM is a File Integrity Monitoring tool that tracks any event over your files. It is capable of keeping historical data of your files. It checks the filesystem changes in the background. 

FIM is the fastest alternative to other software like Ossec, which performs file integrity monitoring. It could integrate with other security tools. The produced data can be ingested and analyzed with tools like ElasticSearch/OpenSearch. It has developed with Rust, a popular programming language.

---

Available features:

- *File watcher*. FIM will emit events on any produced action over your files. It will enhance your environment to the next level of security.
- *Real time alerting*. FIM works in real time. Any change in your files will trigger at the moment.
- *Fast and reliable*. With rust language at the heart of FIM code. It allows us to produce faster, safer and more reliable code.
- *Ingester integrated*. FIM supports native events sent to any current indexer like OpenSearch, ElasticSearch and Wazuh indexer. Enhance your experience.
- *Identification of changes* in content, attributes, ownership or permissions.
- *Extended detected event data*, using Audit Linux daemon. Retrieve who produces an event and which command produces it.
- *Historical logs* storage of detected events.
- *File integrity checking*. Automated file integrity hash production. FIM will analyze each file change.
- Compatible with Linux, macOS and Windows.
- *Open Source software*. Our software is developed as a completely free open-source model. It includes a TDD methodology to produce better software.

--- 

# How to install FIM

The FIM package does not require additional software to work. With the FIM package, you will cover all the main features.

If you want to apply data analysis over the events, then install [OpenSearch](https://opensearch.org/downloads.html) software. It will bring tools to ingest and analyze the events produced by FIM.

Go to our [Installation guide]({% link docs/installation-guide.md %}) to install FIM in your host.