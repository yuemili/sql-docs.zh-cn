---
title: MSmerge_tombstone （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_tombstone_TSQL
- MSmerge_tombstone
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_tombstone system table
ms.assetid: 8b3fc7bf-729b-40f2-8a26-e7dfbe8ddb38
author: stevestein
ms.author: sstein
ms.openlocfilehash: 12caefe8b764090d46051912c876272c9efe86bd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68092658"
---
# <a name="msmerge_tombstone-transact-sql"></a>MSmerge_tombstone (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_tombstone**表包含有关已删除行的信息，并允许将删除传播到其他订阅服务器。 该表存储在发布数据库和订阅数据库中。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**rowguid**|**uniqueidentifier**|行标识符。|  
|**tablenick**|**int**|表的别名。|  
|type |**tinyint**|删除的类型：<br /><br /> 1 = 用户删除。<br /><br /> 5 = 行不再属于筛选分区。<br /><br /> 6 = 系统删除。|  
|**衍生**|**varbinary （249）**|指示被删除的记录的版本，以及删除此记录时已知的更新。 出现两台订阅服务器在同一时间分别对一个行执行更新和删除操作的情况时，允许规则执行一致的冲突解决。|  
|**产生**|**int**|在删除行时赋值。 如果订阅服务器请求第 N 代，则只发送代 >= N 的逻辑删除。|  
|**logical_record_parent_rowguid**|**uniqueidentifier**|标识被删除的行所属的逻辑记录。|  
|**logical_record_lineage**|**Varbinary （501）**|订阅服务器别名和版本号对，用于维护此行所属的逻辑记录的删除历史记录。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
