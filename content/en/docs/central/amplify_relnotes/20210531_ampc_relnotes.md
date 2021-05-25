---
title: Amplify Central May 2021 Release Notes
linkTitle: Amplify Central May 2021
weight: 90
date: 2021-05-17
description: Amplify Central enables the user to manage their provider /
  consumer view. For more information, see the Amplify Central documentation.
---
## New features and enhancements

The following new features and enhancements are available in this update.

### Axway Central CLI

The Axway Central CLI is a package for managing Amplify Central resources with a DevOps approach to API Management.

Axway Central CLI version 1.10.0 is now available on NPM (<https://www.npmjs.com/package/@axway/axway-central-cli/v/1.10.0>).

The CLI extension is compatible with the Axway CLI **version 2.1** (<https://www.npmjs.com/package/axway/v/2.1.0>).

**This is also backward compatible with the Amplify CLI 1.4**.

The Axway Central CLI includes the following enhancements:

* Add enhancement here.

### Amplify Central WebUI

The Amplify Central WebUI is used by both the API providers and consumers to manage and consume APIs.

The Amplify Central WebUI includes the following enhancements:  

* The developer role has access to the environment (read-only) and API services (create/read/update/delete).
* Central Administrator can edit the environment details and update image, title,tags and attributes.

### Axway APIM Gateway / AWS / Azure agents

To provide better visibility into your multi-type gateway eco system, two sets of agents are provided. These agents collect data from the Gateway (API / traffic) and expose it in Amplify Central, providing you with a global vision of your eco system from a single interface.

The agents include the following enhancements:

* **Transaction sampling**: Traceability agent are now able to sample the transactions they are sending to Amplify platform. The sampling can be done globally across all APIs (`TRACEABILITY_SAMPLING_PER_API=false`) or per API (`TRACEABILITY_SAMPLING_PER_API=true`). The variable `TRACEABILITY_SAMPLING_PERCENTAGE` allow to select which transaction percentage should be sent. By default all transactions are sent to Amplify platform. The transactions in error are always sent to the platform. This can be deactivated using `TRACEABILITY_REPORTALLERRORS=false` variable. If you deactivate the error reporting, then the transaction in error will be considered in the sampling mechanism. Refer to [Trace sampling](/docs/central/connected_agent_common_reference/trace_sampling)
* **Usage report**: The Traceability agent is able to track the API usage and report it to Amplify platform. The usage is visible in the Platform UI > Organization > Usage. Refer to [Traceability usage](/docs/central/connected_agent_common_reference/trace_sampling)
* **Transaction redaction**: You can change the masking characters with the environment variable `TRACEABILITY_REDACTION_MASKING_CHARACTERS`. Acceptable characters are alphanumeric, between 1-5 characters, and can contain '-' (hyphen), '*' (star), '#' (sharp), '^' (caret), '~' (tilde), '.' (dot), '{' (open curly bracket), and '}' (closing curly bracket) only. Default value is `{*}`.
* The subscription application drop down propose all Axway Gateway applications having access to the API matching the selected catalog asset.
* The discovery and traceability agents have a new property `CENTRAL_REPORTACTIVITYFREQUENCY` that allows to select the frequency used to report their status to Amplify platform. Default value is 5min.

### Amplify Central API

A new Amplify Central Traceability API is now available for for dynamically querying traffic metrics directly. This API is based on the Lexus query API used in mobile analytics and can be used to retrieve raw metrics for API usage, return codes, and call graph details. It provides filtering and aggregation on any transaction attribute.

The Amplify Central API includes the following enhancements:

* Add enhancement here.

### Mesh Governance / Istio agent

Amplify Central mesh governance enables you to govern and manage your APIs, public and private services, along with the hybrid environments where they are located.

Mesh Governance includes the following enhancements:

* None.

## Fixed issues

The following issues are fixed in this version of Amplify Central:

* **Azure discovery agent adds (Azure) to the service name**. Previously, when an API was discovered by Azure discovery agent, "(Azure)" was added to the Catalog item. Now, only the environment name is added to the Catalog item.
* **Agents terminate if API Manager system is unreachable on startup**. Previously, when starting the v7 agents in service mode, if the API Gateway and/or API Manager is not ready, the Discovery and Traceability agents stopped. Now, the service mode has a retry mechanism in order to succeed to start as soon as API Manager system is available. You need to update existing Linux service running the following command: `sudo ./discovery_agent service update -u axway -g axway --envFile /path/to/da_env_file.env` or `sudo ./traceability_agent service update -u axway -g axway --envFile /path/to/ta_env_file.env`. This will remove existing service and re-create the service with appropriate parameters.
* **Discovery agent does not remove API Service when API is removed in Axway API Manager**. Previously, when an API was deleted in Axway API Manager, the Catalog item was removed but the API service was not. Now, both Catalog item and API service are removed.
* **Azure trace are not pushed to Condor: "empty url"**. Previously when an authentication error occurred on Azure Gateway (401 http code), the Azure traceability agent failed to catch correctly the error and displayed "empty url" in logs. Now, the error are correctly handled and the transaction is visible in API Observer.
* **Prevent running multiple instances of an agent on the same machine**. Previously it was possible to start several time a v7 binary agent on the same machine leading to bad agent behavior. Now, using the agent healthcheck, only one instance of a v7 agent can be started on the same machine.
* **Installing traceability agent only for v7 asks you for disco agent name**. Previously, when installing v7 traceability agent alone, CLI asked you to enter a discovery agent name. Now, only the traceability agent name is asked.

## Known limitations

This version of Amplify Central has the following limitations:

* API Observer:

    * Users that are assigned the Consumer role cannot see their subscription usage on the API Observer screen.

* Axway APIM Gateway agents:

    * Discovery Agent cannot expose discovered APIs in multiple teams, so the organization structure on API Manager is lost in Amplify Central. As a result, the API provider must create the team in Amplify platform and share the API within the appropriate teams.
    * When an API is renamed on the API Manager, the Discovery Agent is not able to recognize the API name change. This results in the API displaying in Amplify Central with dual entries of both the originally discovered name and the newly changed name.
    * Traceability Agent is working in an Externally Managed Topology (EMT) deployment but it is not able to report the transaction request/response headers as the API to collect them are not accessible in EMT mode.

* AWS Gateway agents:

    * Discovery Agent is working with only one AWS Region (the one used when installing the agent).
    * Discovery Agent can discover APIs having ANY method only, but consumers will not be able to subscribe to it from Unified Catalog.
    * Discovery Agent does not associate the usage plan and API when a subscriber chooses a usage plan that is not already linked to the chosen API.
    * Usage report in not scalable as the agent rely on AWS Simple Queue Service that cannot have more than 10 consumer per queues. It is possible to increase the number of workers on the agent side

* Azure agents:

    * Discovery Agent does not manage revision and version.
    * Discovery agent does not remove API Service and Catalog item when Azure API is removed.
