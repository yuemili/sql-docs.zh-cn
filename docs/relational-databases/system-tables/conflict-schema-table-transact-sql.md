---
title: "conflict_&lt;架构&gt;_&lt;表&gt;(Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/15/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- conflict_
- conflict_TSQL
dev_langs: TSQL
helpviewer_keywords: conflict_<schema>_<table>
ms.assetid: 15ddd536-db03-454e-b9b5-36efe1f756d7
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cfb2f078495256ee53d021bb09801323bdca094f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="conflictltschemagtlttablegt-transact-sql"></a>conflict_&lt;架构&gt;_&lt;表&gt;(TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Conflict_\<架构 > _\<表 > 表包含有关对等复制中发生冲突的行信息。 发布中的每个复制表都存在一个冲突表，冲突表的名称附加了架构和项目名称。 这些项目特定的冲突表存在于每个发布数据库中。  
  
 对于对等复制，默认情况下，分发代理在检测到冲突时将会失败。 冲突错误会记录到错误日志中，但是冲突数据不会记录到冲突表中；因此没有可供查看的冲突数据。 如果允许分发代理继续运行，将在检测到冲突的每个节点本地记录冲突。 有关详细信息，请参阅 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)中的“处理冲突”。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|__$originator_id|**int**|发起冲突更改的节点的 ID。 有关 Id 的列表，执行[sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md)。|  
|__$origin_datasource|**int**|发起冲突更改的节点。|  
|__$tranid|**nvarchar (40)**|在 __$origin_datasource 中应用的冲突更改的日志序列号 (LSN)。|  
|__$conflict_type|**int**|冲突类型，可以是下列值之一：<br /><br /> 1：更新失败，因为另一个更新已更改了本地行，或者删除了本地行并随后重新插入。<br /><br /> 2：更改失败，因为已删除了本地行。<br /><br /> 3：删除失败，因为另一个更新已更改了本地行，或者删除了本地行并随后重新插入。<br /><br /> 4：删除失败，因为已删除了本地行。<br /><br /> 5：插入失败，因为已插入了本地行，或者已插入并随后更新了本地行。|  
|__$is_winner|**bit**|指示该表中的行是否为冲突入选方，这意味着将其应用于本地节点。|  
|__$pre_version|**varbinary (32)**|发起冲突更改的数据库的版本。|  
|__$reason_code|**int**|冲突的解决代码。 可以是以下值之一：<br /><br /> 0<br /><br /> 1<br /><br /> 2<br /><br /> <br /><br /> 有关详细信息，请参阅**__ reason_text**。|  
|__$reason_text|**nvarchar (720)**|冲突的解决情况。 可以是以下值之一：<br /><br /> 已解决 (1)<br /><br /> 未解决 (2)<br /><br /> 未知 (0)|  
|__$update_bitmap|**varbinary (**  *n*  **)**。 大小不同而有所不同，具体取决于内容。|一个位图，指示在发生更新-更新冲突的情况下更新的列。|  
|__$inserted_date|**datetime**|将冲突行插入此表中的日期和时间。|  
|__$row_id|**timestamp**|与导致冲突的行关联的行版本。|  
|__$change_id|**binary (8)**|对于本地行，该值等于与本地行发生冲突的传入行的 __$row_id。 对于传入行，该值为 NULL。|  
|\<基础表的列名称 >|\<基表列类型 >|在冲突表中，基表中的每一列都有一个对应的列。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  