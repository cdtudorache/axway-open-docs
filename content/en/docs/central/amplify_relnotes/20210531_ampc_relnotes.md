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

Axway Central CLI version 1.9.0 is now available on NPM (<https://www.npmjs.com/package/@axway/axway-central-cli/v/1.9.0>).

The CLI extension is compatible with the Axway CLI **version 2.0** (<https://www.npmjs.com/package/axway/v/2.0.0>).

**This is also backward compatible with the Amplify CLI 1.4**.

The Axway Central CLI includes the following enhancements:

* Add enhancement here.

### Amplify Central WebUI

The Amplify Central WebUI is used by both the API providers and consumers to manage and consume APIs.

The Amplify Central WebUI includes the following enhancements:  

* Add enhancement here.

### Axway APIM Gateway / AWS / Azure agents

To provide better visibility into your multi-type gateway eco system, two sets of agents are provided. These agents collect data from the Gateway (API / traffic) and expose it in Amplify Central, providing you with a global vision of your eco system from a single interface.

The agents include the following enhancements:

* Add enhancement here.

### Amplify Central API

A new Amplify Central Traceability API is now available for for dynamically querying traffic metrics directly. This API is based on the Lexus query API used in mobile analytics and can be used to retrieve raw metrics for API usage, return codes, and call graph details. It provides filtering and aggregation on any transaction attribute.

The Amplify Central API includes the following enhancements:

* Add enhancement here.

### Mesh Governance / Istio agent

Amplify Central mesh governance enables you to govern and manage your APIs, public and private services, along with the hybrid environments where they are located.

Mesh Governance includes the following enhancements:

* Add enhancement here.

## Fixed issues

The following issues are fixed in this version of Amplify Central:

* **Add fixed issue here**. Previously,

## Known limitations

This version of Amplify Central has the following limitations:

* API Observer:

    * Users that are assigned the Consumer role cannot see their subscription usage on the API Observer screen.

* Axway APIM Gateway agents:

    * When starting the agent, if the API Gateway and/or API Manager is not ready, the Discovery and Traceability agents will stop. When using Linux service mode, it is possible that the agent fails to start because API Manager/Gateway are not started yet. This can lead to a bad status display in the corresponding environment in Central UI > Topology.
    * Discovery Agent cannot expose discovered APIs in multiple teams, so the organization structure on API Manager is lost in Amplify Central. As a result, the API provider must create the team in Amplify platform and share the API within the appropriate teams.
    * When an API is renamed on the API Manager, the Discovery Agent is not able to recognize the API name change. This results in the API displaying in Amplify Central with dual entries of both the originally discovered name and the newly changed name.
    * Traceability Agent is working in an externally managed topology deployment only if you deactivate the headers details (`APIGATEWAY_GETHEADERS=false`).

* AWS Gateway agents:

    * Discovery Agent is working with only one AWS Region (the one used when installing the agent).
    * Discovery Agent can discover APIs having ANY method only, but consumers will not be able to subscribe to it from Unified Catalog.
    * Discovery Agent does not associate the usage plan and API when a subscriber chooses a usage plan that is not already linked to the chosen API.

* Azure agents:

    * Discovery Agent does not manage revision and version.
    * Discovery agent does not remove API Service and Catalog item when Azure API is removed.