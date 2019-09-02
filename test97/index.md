---
title: 'Administrar la conmutación por error del grupo de disponibilidad: SQL Server en Linux'
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: a13f9f3da00889323f3d971ffd801f1fa7d09890
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68027218"
---
# <a name="always-on-availability-group-failover-on-linux"></a>Conmutación por error del grupo de disponibilidad Always On en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dentro del contexto de un grupo de disponibilidad, el rol principal y el rol secundario de las réplicas de disponibilidad suelen ser intercambiables en un proceso denominado conmutación por error. Hay tres formas de conmutación por error: conmutación por error automática (sin pérdida de datos), conmutación por error manual planeada (sin pérdida de datos) y conmutación por error manual forzada (con posible pérdida de datos), normalmente denominada *conmutación por error forzada*. Las conmutaciones por error automáticas o manuales planeadas conservan todos los datos. Un grupo de disponibilidad conmuta por error en el nivel de la réplica de disponibilidad. Es decir, un grupo de disponibilidad conmuta por error en una de sus réplicas secundarias (el destino de la conmutación por error actual). 

Para obtener información general sobre la conmutación por error, vea [Conmutación por error y modos de conmutación por error](../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md).

## <a name="failover"></a>Conmutación por error manual

Use las herramientas de administración de clústeres para conmutar por error un grupo de disponibilidad administrado por un administrador de clústeres externo. Por ejemplo, si una solución usa Pacemaker para administrar un clúster de Linux, use `pcs` para realizar las conmutaciones por error manuales en RHEL o Ubuntu. En SLES, use `crm`. 

> [!IMPORTANT]
> En las operaciones normales, no conmute por error con las herramientas de administración de SQL Server o Transact-SQL, como SSMS o PowerShell. Cuando `CLUSTER_TYPE = EXTERNAL`, el único valor aceptable para `FAILOVER_MODE` es `EXTERNAL`. Con esta configuración, el administrador de clústeres externo ejecuta todas las acciones de conmutación por error manuales o automáticas. Para obtener instrucciones sobre cómo forzar la conmutación por error con una posible pérdida de datos, vea [Forzar la conmutación por error](#forceFailover).

### <a name="a-namemanualfailovermanual-failover-steps"></a><a name="manualFailover">Pasos de una conmutación por error manual

Para conmutar por error, la réplica secundaria que se convertirá en la réplica principal tiene que ser sincrónica. Si una réplica secundaria es asincrónica, [cambie el modo de disponibilidad](../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md).

Conmute por error de forma manual en dos pasos.

   Primero, [conmute por error de forma manual al mover el recurso del grupo de disponibilidad](#manualMove) desde el nodo del clúster propietario de los recursos a un nodo nuevo.

   El clúster conmutará por error el recurso del grupo de disponibilidad y agregará una restricción de ubicación. Esta restricción configura el recurso para ejecutarse en el nuevo nodo. Quite esta restricción para conmutar por error correctamente en el futuro.

   En segundo lugar, [quite la restricción de ubicación](#removeLocConstraint).

#### <a name="a-namemanualmovestep-1-manually-fail-over-by-moving-availability-group-resource"></a><a name="manualMove">Paso 1. Conmutar por error de forma manual al mover el recurso de un grupo de disponibilidad

Para conmutar por error de forma manual el recurso de un grupo de disponibilidad denominado *ag_cluster* a un nodo de clúster denominado *nodeName2*, ejecute el comando adecuado para su distribución:
