[[_TOC_]]

## Overview

Service connections provide access to external resources such as Azure for executing tasks in a job.

## Naming Convention

Consider the following naming convention for service connections: `{Name_of_SPN}-{?environment}-arm`

> NOTE: If the name of the underlying SPN already includes the environment affix, consider not adding it again to the service connection name.

## Connections by Environment

Each environment will have a set of service connections in order to manage access to the Azure subscription for that given environment.

There will be 3 service connections per environment:

1. DPH - Manages deployment of resources into DPH Azure subscription.
1. DMH - Manages deployment of resources into DMH Azure subscription.
1. Shared - Manages deployment of resources into shared Azure subscription.

## Permissions

- `Endpoint Administrators` and the creator of the service connection will have access to manage existing service connections.
- Only the current project will have access to the service connection.
- Only selected pipelines will have access to the service connection.