---
title: SQL Server 代理属性（“作业系统”页）
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.job.f1
ms.assetid: e171d13e-1302-4f0e-88be-67d656aec8d3
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1e68f009e832dceb9ff1ac074b62c38ac4f2de8b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247552"
---
# <a name="sql-server-agent-properties-job-system-page"></a>SQL Server 代理属性（“作业系统”页）
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此页，可以查看和修改 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务如何管理作业。  
  
## <a name="options"></a>选项  
**关闭超时间隔(秒)**  
指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理在关闭作业之前等待作业完成的秒数。 如果在指定间隔之后作业仍在运行，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将强制停止该作业。  
  
**使用非管理员代理帐户**  
为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理设置非管理员代理帐户。 因为 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] 及更高版本支持多个代理，所以仅当管理版本低于 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理时，此选项才适用。  
  
**用户名**  
键入非管理员代理帐户的用户名。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持多个代理，所以仅当管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]代理版本时此选项才适用。  
  
**密码**  
键入非管理员代理帐户的用户密码。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更高版本支持多个代理，因此，仅当管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]代理版本时此选项才适用。  
  
**域**  
键入非管理性代理帐户的用户域。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持多个代理，所以仅当管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]代理版本时此选项才适用。  
  
## <a name="see-also"></a>另请参阅  
[执行作业](../../ssms/agent/implement-jobs.md)  
  
