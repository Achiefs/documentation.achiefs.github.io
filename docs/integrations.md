---
layout: default
title: Integrations
nav_order: 5
---

# Integrations
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

---

# Summary

FIM supports integration with two platforms (one at the same time). The integration will help users to store in the cloud all the events produced by FIM in a easy way. The stored events could be processed and analyzed lately.

---

# Supported integrations

FIM supports two integrations:
- ElasticSearch 8.x or OpenSearch 2.x
- Splunk indexer 9.x

---

# ElasticSearch/OpenSearch integration configuration

The ELS/OS integration is set by the `endpoint` configuration section. This section has different options, but the required ones are the following:
- ElasticSearch/OpenSearch `address`. This address has to be addressable by the FIM node. The `address` usually includes the port that ELS/OS by default uses the 9200, an example of the `address` field: `https://elastic.example.com:9200`.

{: .note}
> Review the `insecure` parameter in a testing environment. In the production environment, you should use `insecure: false` or keep it empty as default `false`.

- Inside the credentials section, it's required to set the `user` and `password` parameters to access the indexer environment.
  - The `user` parameter has to contain an ELS/OS username with permission to push an object into an index and create an index.
  - The `password` parameter has to contain the access password of the previously given user.

{: .note}
> To see all endpoint parameters take a look at [Configuration file]({% link docs/configuration-file.md %})

Those are all the required steps to start working with ElasticSearch or OpenSearch indexer tools. FIM will create the index of the day called `fim-yyyy-mm-dd`. Any produced event that FIM detects will be in this index.

---

# Splunk integration configuration

The Splunk integration is set by the `endpoint` configuration section. This section has different options. In addition, the Splunk integration will require additional steps to receive FIM events into the Splunk indexer. The steps are the following:

First, it is required to configure the Splunk indexer to accept FIM events.

1. At the Splunk home page, click on the `Settings` tab.
![Splunk home page](../../assets/images/splunk/home.png)

2. Select the `indexes` setting inside the panel.
![Settings panel with indexes highlighted](../../assets/images/splunk/home_settings_indexes.png)

3. Click on the `New Index` button to create the FIM index.
![Indexes page](../../assets/images/splunk/indexes.png)

4. The name of the index must be `fim_events` do not change please, click on `Save`.
![New index dialog](../../assets/images/splunk/new_index.png)

5. Go to the `Settings` tab and click on `Data inputs`.
![Settings panel with data inputs highlighted](../../assets/images/splunk/home_settings_data_inputs.png)

6. Click on `+ Add new` to add a new HTTP Event Collector item.
![Data inputs page](../../assets/images/splunk/data_inputs.png)

7. Set your HTTP Event Collector name as you wish, and click on `Next`.
![HTTP Event Collector first dialog](../../assets/images/splunk/new_collector.png)

8. Give the collector permission to push into the `fim_events` index, set it as the default index, and click on `Review`.
![HTTP Event Collector index selector](../../assets/images/splunk/new_collector_index.png)

9. Review your configuration and click on `Submit`.
![HTTP Event Collector review page](../../assets/images/splunk/new_collector_submit.png)

10. Splunk gives the token required in FIM configuration to push events into Splunk, copy the token and keep it secret.
![HTTP Event Collector token page](../../assets/images/splunk/collector_token.png)

11. Configure the endpoint address with the default HTTP event collector `8088` and the token obtained in the previous step.

{: .note}
> The HTTP Event Collector works by default in HTTPS mode. So, FIM needs to contain the `https://` address in the configuration file.

Those are all the required steps to start working with Splunk indexer tools. Any produced event that FIM detects will be in this index.

---
