---
title: 高可用性支持 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2e0f6d3f-0536-46d9-8630-835e199515bf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d948a9edfafdbf39bd8ee5c512fb77814cb7adf7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62837252"
---
# <a name="high-availability-support"></a>高可用性支持
  Oracle CDC 服务是为高可用性而设计的。 下列功能为高可用性支持助一臂之力：  
  
-   Oracle CDC 服务不占用任何文件资源（本地资源或其他资源）。 其整个状态都存储于目标 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中。 因此，如果运行该服务的计算机失败，可以轻松地在使用相同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的其他计算机上启动该服务。 为了缩短恢复时间，长的或长时间运行的 Oracle 事务保存在目标 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的临时表中，从而无需在失败（或服务重新启动）后重新扫描许多 Oracle 事务日志。  
  
-   Oracle CDC 服务可以使用群集的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，因此，它可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例故障转移到其他群集节点后恢复。 Oracle CDC 服务计算机管理员仅需在创建 Oracle CDC 服务时指定与群集的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的连接信息。  
  
-   Oracle CDC 服务可以使用[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] **AlwaysOn**数据库镜像功能。 此支持要求 MSXDBCDC 和所有 CDC 数据库都位于同一个可用性组中。 它还要求 Oracle CDC 服务计算机管理员为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可用性组指定适当的`Failover_Partner and Network=dbmssocn` **AlwaysOn**连接信息（例如，连接属性）。 这允许 CDC 服务在故障转移后自动恢复在数据库的辅助副本上的处理。  
  
-   Oracle CDC 服务可以配置为 Windows 故障转移群集上的一般服务资源（可与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一起也可以独立于后者），从而可以轻松地故障转移和回退针对群集的 CDC 处理。 若要将某一 Oracle CDC 服务配置为某个故障转移群集中的资源，系统管理员必须将该 Oracle CDC 服务配置为该故障转移群集上各节点的一般服务资源。  
  
-   Oracle CDC 服务支持 Oracle RAC，这允许其与 Oracle 数据库进行通信并且甚至在某一 Oracle RAC 节点停机时处理日志。  
  
  
