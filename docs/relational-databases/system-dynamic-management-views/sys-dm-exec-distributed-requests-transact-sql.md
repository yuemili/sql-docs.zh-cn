---
title: sys. dm_exec_distributed_requests （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DISTRIBUTED_REQUESTS
- DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
- SYS.DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- sys.dm_exec_distributed_sql_requests management view
- PolyBase
- dm_exec_distributed_sql_requests management view
ms.assetid: c041d416-d8c6-435e-a563-6a310abd33e3
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 37fd17f17d8b6aa1a30f48d75258d27f4a45561a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68097799"
---
# <a name="sysdm_exec_distributed_requests-transact-sql"></a>sys.dm_exec_distributed_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  保存有关 PolyBase 查询中当前或最近活动的所有请求的信息。 每个请求/查询在表中各占一行。  
  
 用户随后可以根据会话和请求 ID 检索生成的、通过 sys.databases 执行的实际分布式请求。 dm_exec_distributed_requests。 例如，涉及常规 SQL 表和外部 SQL 表的查询将分解为跨各种计算节点执行的各种语句/请求。 为了跟踪所有计算节点上的分布式步骤，我们引入了一个 "全局" 执行 ID，该 ID 可用于跟踪与一个特定请求和运算符关联的计算节点上的所有操作。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|sql_handle|**varbinary （64）**|此视图的键。 与请求关联的唯一数字 id。|系统中所有请求都是唯一的。|  
|execution_id|**nvarchar （32**|与运行此查询的会话相关联的唯一数字 id。||  
|status|**nvarchar （32**|请求的当前状态。|"挂起"、"授权"、"AcquireSystemResources"、"正在初始化"、"计划"、"正在分析"、"AquireResources"、"正在运行"、"正在取消"、"完成"、"失败"、"已取消"。|  
|error_id|**nvarchar （36）**|与请求关联的错误的唯一 id （如果有）。|如果未发生错误，则设置为 NULL。|  
|start_time|**datetime**|开始执行请求的时间。|对于排队请求，为 0;否则，有效的日期时间小于或等于当前时间。|  
|end_time|**datetime**|引擎完成编译请求的时间。|对于排队或活动的请求为 Null;否则，有效的日期时间小于或等于当前时间。|  
|total_elapsed_time|**int**|自请求开始后执行所用的时间（以毫秒为单位）。|介于0与 start_time 与 end_time 之间的差异。如果 total_elapsed_time 超过整数的最大值，则 total_elapsed_time 将继续作为最大值。 此条件将生成警告 "已超过最大值。" 最大值（以毫秒为单位）等效于24.8 天。|  
  
## <a name="see-also"></a>另请参阅  
 [通过动态管理视图进行 PolyBase 故障排除](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
