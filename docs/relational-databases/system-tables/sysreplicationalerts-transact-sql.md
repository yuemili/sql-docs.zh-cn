---
title: sysreplicationalerts （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysreplicationalerts_TSQL
- sysreplicationalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysreplicationalerts system table
ms.assetid: 6ed15828-8cca-4cf0-b2ff-1ecd0d8db11a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6cbeab4c673390cb80300eb5ced2b4cb5c1bcf1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029746"
---
# <a name="sysreplicationalerts-transact-sql"></a>sysreplicationalerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含导致激发复制警报的情况的相关信息。 该表存储在**msdb**数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|警报的 ID。|  
|**状态值**|**int**|用户定义的值：<br /><br /> **0** = 通往。<br /><br /> **1** = 服务。|  
|**agent_type**|**int**|代理类型：<br /><br /> **1** = 快照代理。<br /><br /> **2** = 日志读取器代理。<br /><br /> **3** = 分发代理。<br /><br /> **4** = 合并代理。|  
|**agent_id**|**int**|表中的代理 ID **MSsnapshot_agents**、 **MSlogreader_agents**、 **MSdistribution_agents**或**MSmerge_agents**。|  
|**error_id**|**int**|存储在**MSrepl_errors**中的错误的 ID。|  
|**alert_error_code**|**int**|将此记录记入日志时所引发警报的消息 ID。|  
|**time**|**datetime**|插入记录的时间。|  
|**器**|**sysname**|与激发此警报的代理相关联的发布服务器的名称。|  
|**publisher_db**|**sysname**|与激发此警报的代理相关联的发布服务器数据库。|  
|**发布**|**sysname**|与激发此警报的代理相关联的发布。|  
|**publication_type**|**int**|发布类型：<br /><br /> **0** = Snapshot。<br /><br /> **1** = 事务性。<br /><br /> **2** = 合并。|  
|**订阅服务器**|**sysname**|与激发此警报的代理相关联的订阅服务器的名称。|  
|**subscriber_db**|**sysname**|与激发此警报的代理相关联的订阅服务器数据库的名称。|  
|**下文**|**sysname**|与激发此警报的代理相关联的项目的名称。|  
|**destination_object**|**sysname**|与此警报相关联的订阅表的名称。|  
|**source_object**|**sysname**|与此警报相关联的已发布表的名称。|  
|**alert_error_text**|**ntext**|警报的文本。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
