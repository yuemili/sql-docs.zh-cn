---
title: log_shipping_monitor_history_detail （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_history_detail_TSQL
- log_shipping_monitor_history_detail
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_monitor_history_detail system table
ms.assetid: 7080c888-323b-4206-a1ab-e6c51f9e2579
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0f0a304020b972b29d521bd32da3f98b8d3fdfc9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67989991"
---
# <a name="log_shipping_monitor_history_detail-transact-sql"></a>log_shipping_monitor_history_detail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  存储日志传送作业的历史记录详细信息。 该表存储在**msdb**数据库中。  
  
 与历史记录和监视相关的表也用于主服务器和辅助服务器。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**agent_id**|**uniqueidentifier**|用于备份的主 ID 或者用于复制或还原的辅助 ID。|  
|**agent_type**|**tinyint**|日志传送作业的类型。<br /><br /> 0 = 备份。<br /><br /> 1 = 复制。<br /><br /> 2 = 还原。|  
|**session_id**|**int**|备份/复制/还原作业的会话 ID。|  
|**database_name**|**sysname**|与此记录关联的数据库的名称。 用于备份的主数据库、用于还原的辅助数据库或用于复制的空数据库。|  
|**session_status**|**tinyint**|会话的状态。<br /><br /> 0 = 正在启动。<br /><br /> 1 = 正在运行。<br /><br /> 2 = 成功。<br /><br /> 3 = 错误。<br /><br /> 4 = 警告。|  
|**log_time**|**datetime**|创建记录的日期和时间。|  
|**log_time_utc**|**datetime**|创建记录的日期和时间，使用通用协调时间表示。|  
|**消息**|**nvarchar(max)**|消息正文。|  
  
## <a name="remarks"></a>备注  
 此表包含日志传送代理的历史记录详细信息。 若要标识代理会话，请使用列**agent_id**、 **agent_type**和**session_id**。 若要查看代理会话的历史记录详细信息，请按**log_time**排序。  
  
 除了存储在远程监视服务器上外，与主服务器有关的信息存储在主服务器上的**log_shipping_monitor_history_detail**表中，与辅助服务器相关的信息也存储在辅助服务器上的**log_shipping_monitor_history_detail**表中。  
  
## <a name="see-also"></a>另请参阅  
 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_delete_log_shipping_primary_database &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_cleanup_log_shipping_history &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [系统表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [log_shipping_monitor_error_detail &#40;Transact-sql&#41;](../../relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql.md)  
  
  
