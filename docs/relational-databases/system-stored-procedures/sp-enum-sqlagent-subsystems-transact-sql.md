---
title: sp_enum_sqlagent_subsystems （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_sqlagent_subsystems
- sp_enum_sqlagent_subsystems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_sqlagent_subsystems
ms.assetid: 019a3c9d-bac3-495b-a70a-2c19f1d2e20e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 963cbcea93091eb48b8c73214ee3bc509f118e67
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68124664"
---
# <a name="sp_enum_sqlagent_subsystems-transact-sql"></a>sp_enum_sqlagent_subsystems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理子系统。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_enum_sqlagent_subsystems  
```  
  
## <a name="arguments"></a>参数  
 无  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**适用**|**nvarchar （40）**|子系统的名称。|  
|**2008**|**nvarchar(512)**|对子系统的说明。|  
|**subsystem_dll**|**nvarchar （510）**|包含子系统的 DLL 模块。|  
|**agent_exe**|**nvarchar （510）**|子系统所用的可执行模块。|  
|**start_entry_point**|**nvarchar （30）**|在作业步骤执行期间 SQL Server 代理调用的过程。|  
|**event_entry_point**|**nvarchar （30）**|在作业步骤执行期间 SQL Server 代理调用的过程。|  
|**stop_entry_point**|**nvarchar （30）**|在作业步骤执行期间 SQL Server 代理调用的过程。|  
|**max_worker_threads**|**int**|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将为此子系统启动的最大线程数。|  
|**subsystem_id**|**int**|子系统的标识符。|  
  
## <a name="remarks"></a>备注  
 此过程列出实例中可用的子系统。  
  
## <a name="permissions"></a>权限  
 默认情况下， **sysadmin**固定服务器角色的成员可以执行此存储过程。 其他用户必须被授予 **msdb** 数据库中的 **SQLAgentOperatorRole** 固定数据库角色的权限。  
  
 有关**SQLAgentOperatorRole**的详细信息，请参阅[SQL Server 代理固定数据库角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
## <a name="see-also"></a>另请参阅  
 [实现 SQL Server 代理安全性](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_add_jobstep (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
  
  
