---
title: Manage availability group failover - SQL Server on Linux
description: 
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 
---
For background information about failover, see [Failover and failover modes](../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md).

## <a name="failover"></a>Manual failover

Use the cluster management tools to fail over an AG managed by an external cluster manager. For example, if a solution uses Pacemaker to manage a Linux cluster, use `pcs` to perform manual failovers on RHEL or Ubuntu. On SLES use `crm`. 

> [!IMPORTANT]
> Under normal operations, do not fail over with Transact-SQL or SQL Server management tools like SSMS or PowerShell. When `CLUSTER_TYPE = EXTERNAL`, the only acceptable value for `FAILOVER_MODE` is `EXTERNAL`. With these settings, all manual or automatic failover actions are executed by the external cluster manager. For instructions to force failover with potential data loss, see [Force failover](#forceFailover).

### <a name="manualFailover">Manual failover steps

To fail over, the secondary replica that will become the primary replica must be synchronous. If a secondary replica is asynchronous, [change the availability mode](../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md).

Manually fail over in two steps.

   First, [manually fail over by moving AG resource](#manualMove) from the cluster node that owns the resources to a new node.

   The cluster fails the AG resource over and adds a location constraint. This constraint configures the resource to run on the new node. Remove this constraint in order to successfully fail over in the future.

   Second, [remove the location constraint](#removeLocConstraint).

#### <a name="manualMove">Step 1. Manually fail over by moving availability group resource

To manually fail over an AG resource named *ag_cluster* to cluster node named *nodeName2*, run the appropriate command for your distribution:
