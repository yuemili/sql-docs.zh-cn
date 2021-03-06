---
title: sys. dm_resource_governor_workload_groups （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_workload_groups
- sys.dm_resource_governor_workload_groups_TSQL
- dm_resource_governor_workload_groups
- dm_resource_governor_workload_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_workload_groups dynamic management view
ms.assetid: f63c4914-1272-43ef-b135-fe1aabd953e0
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 73da0ee5a47cf5b1c7443729e2a9b71dc01d18a7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "73982293"
---
# <a name="sysdm_resource_governor_workload_groups-transact-sql"></a>sys.dm_resource_governor_workload_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回工作负荷组统计信息和工作负荷组当前在内存中的配置。 此视图可以与 sys.dm_resource_governor_resource_pools 联接以获取资源池名称。  
  
> [!NOTE]  
>  若要从[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]调用此，请使用名称**dm_pdw_nodes_resource_governor_workload_groups**。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|group_id|**int**|工作负荷组的 ID。 不可为 null。|  
|name|**sysname**|工作负荷组的名称。 不可为 null。|  
|pool_id|**int**|资源池的 ID。 不可为 null。|  
|external_pool_id|**int**|**适用于**：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 及更高版本。<br /><br /> 外部资源池的 ID。 不可为 null。|  
|statistics_start_time|**datetime**|为工作负荷组重置统计信息集合的时间。 不可为 null。|  
|total_request_count|**bigint**|工作负荷组中已完成请求的累计计数。 不可为 null。|  
|total_queued_request_count|**bigint**|达到 GROUP_MAX_REQUESTS 限制之后排队请求的累计计数。 不可为 null。|  
|active_request_count|**int**|当前请求计数。 不可为 null。|  
|queued_request_count|**int**|当前排队请求计数。 不可为 null。|  
|total_cpu_limit_violation_count|**bigint**|超出 CPU 限制的请求累计计数。 不可为 null。|  
|total_cpu_usage_ms|**bigint**|此工作负荷组的累计 CPU 使用情况，以毫秒为单位。 不可为 null。|  
|max_request_cpu_time_ms|**bigint**|单个请求的最大 CPU 使用情况，以毫秒为单位。 不可为 null。<br /><br /> **注意：** 这是一个测量值，不同于 request_max_cpu_time_sec，这是一个可配置的设置。 有关详细信息，请参阅 [CPU Threshold Exceeded 事件类](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)。|  
|blocked_task_count|**int**|已阻塞任务的当前计数。 不可为 null。|  
|total_lock_wait_count|**bigint**|发生的锁等待累计计数。 不可为 null。|  
|total_lock_wait_time_ms|**bigint**|持有锁的时间的累计之和，以毫秒为单位。 不可为 null。|  
|total_query_optimization_count|**bigint**|此工作负荷组中的查询优化累计计数。 不可为 null。|  
|total_suboptimal_plan_generation_count|**bigint**|由于内存不足，在此工作负荷组中出现的不理想计划生成的累计计数。 不可为 null。|  
|total_reduced_memgrant_count|**bigint**|达到了最大查询大小限制的内存授予累计计数。 不可为 null。|  
|max_request_grant_memory_kb|**bigint**|统计信息重置之后单个请求的最大内存授予大小，以千字节为单位。 不可为 null。|  
|active_parallel_thread_count|**bigint**|并行线程使用情况的当前计数。 不可为 null。|  
|importance|**sysname**|此工作负荷组中请求的相对重要性的当前配置值。 重要性为下列值之一，默认值为 "低"、"中" 或 "高"。<br /><br /> 不可为 null。|  
|request_max_memory_grant_percent|**int**|单个请求的最大内存授予的当前设置，以百分比表示。 不可为 null。|  
|request_max_cpu_time_sec|**int**|单个请求的最大 CPU 使用限制的当前设置，以秒为单位。 不可为 null。|  
|request_memory_grant_timeout_sec|**int**|单个请求的内存授予超时的当前设置，以秒为单位。 不可为 null。|  
|group_max_requests|**int**|并发请求最大数的当前设置。 不可为 null。|  
|max_dop|**int**|工作负荷组的最大并行度。 默认值为 0，表示使用全局设置。 不可为 null。|  
|pdw_node_id|**int**|**适用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分发所在的节点的标识符。|  
  
## <a name="remarks"></a>备注  
 此动态管理视图显示了内存中配置。 若要查看存储的配置元数据，请使用 sys.resource_governor_workload_groups 目录视图。  
  
 成功执行 ALTER RESOURCE GOVERNOR RESET STATISTICS 后，会重置以下计数器： statistics_start_time、total_request_count、total_queued_request_count、total_cpu_limit_violation_count、total_cpu_usage_ms、max_request_cpu_time_ms、total_lock_wait_count、total_lock_wait_time_ms、total_query_optimization_count、total_suboptimal_plan_generation_count、total_reduced_memgrant_count 和 max_request_grant_memory_kb。 statistics_start_time 设置为当前系统日期和时间，其他计数器设置为零（0）。  
  
## <a name="permissions"></a>权限  
 需要 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys. dm_resource_governor_resource_pools &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)   
 [sys. resource_governor_workload_groups &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR (Transact-SQL)](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  



