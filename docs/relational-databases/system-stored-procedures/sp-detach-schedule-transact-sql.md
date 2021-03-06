---
title: sp_detach_schedule （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_detach_schedule
- sp_detach_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_detach_schedule
ms.assetid: 9a1fc335-1bef-4638-a33a-771c54a5dd19
author: stevestein
ms.author: sstein
ms.openlocfilehash: aed989cc09922b7b480a7dd7b3ca6820d6b77ab2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67936744"
---
# <a name="sp_detach_schedule-transact-sql"></a>sp_detach_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除计划和作业之间的关联。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_detach_schedule   
     { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
       { [ @schedule_id = ] schedule_id | [ @schedule_name = ] 'schedule_name' } ,  
     [ @delete_unused_schedule = ] delete_unused_schedule   
```  
  
## <a name="arguments"></a>参数  
`[ @job_id = ] job_id`要从中删除计划的作业的标识号。 *job_id*的值为**uniqueidentifier**，默认值为 NULL。  
  
`[ @job_name = ] 'job_name'`要从中删除计划的作业的名称。 *job_name*的默认值为**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  必须指定*job_id*或*job_name* ，但不能同时指定两者。  
  
`[ @schedule_id = ] schedule_id`要从作业中删除的计划的标识号。 *schedule_id*的值为**int**，默认值为 NULL。  
  
`[ @schedule_name = ] 'schedule_name'`要从作业中删除的计划的名称。 *schedule_name*的默认值为**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  必须指定*schedule_id*或*schedule_name* ，但不能同时指定两者。  
  
`[ @delete_unused_schedule = ] delete_unused_schedule`指定是否删除未使用的作业计划。 *delete_unused_schedule*的类型为**bit**，默认值为**0**，这意味着所有计划都将保留，即使没有作业引用它们也是如此。 如果设置为**1**，则会删除未使用的作业计划。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="permissions"></a>权限  
 默认情况下， **sysadmin**固定服务器角色的成员可以执行此存储过程。 其他用户必须被授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **数据库中下列** 代理固定数据库角色的权限之一：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 请注意，作业所有者可以将作业附加到计划以及从计划中分离作业，而不必要求也是计划所有者。 但是，如果分离后导致无作业，除非调用方是计划所有者，否则不能删除计划。  
  
 有关这些角色的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将进行检查以确定用户是否拥有计划。 只有**sysadmin**固定服务器角色的成员才可以从其他用户拥有的作业中分离计划。  
  
## <a name="examples"></a>示例  
 以下示例将删除 `'NightlyJobs'` 计划和 `'BackupDatabase'` 作业之间的关联。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_detach_schedule  
    @job_name = 'BackupDatabase',  
    @schedule_name = 'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)  
  
  
