---
title: 设置作业执行关闭
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
- SQL Server Agent jobs, execution shutdowns
ms.assetid: ac23e88f-53fc-41de-bb16-0c27c002d5a5
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bc6f03f982602c65dc8acab6daa18f2ee385f889
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75253221"
---
# <a name="set-job-execution-shutdown"></a>设置作业执行关闭

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主题说明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理自己结束之前，[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理等待作业执行完的时间。  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Security"></a>安全性  
  
#### <a name="Permissions"></a>Permissions  
默认情况下，sysadmin  固定服务器角色的成员可设置在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理自己结束之前，[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理等待作业执行完的时间。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-set-job-execution-shutdown"></a>设置作业执行关闭  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开要设置作业执行关闭间隔的服务器。  
  
2.  右键单击“SQL Server 代理”  ，然后选择“属性”  。  
  
3.  在 **“选择页”** 下，选择 **“作业系统”** 。  
  
4.  设置“关闭超时间隔(秒)”  以延长或缩短关闭超时间隔。 这决定了在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理本身结束之前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理等待作业执行完成的时间长度。  
  
