---
title: sys. dm_cdc_errors （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_cdc_errors_TSQL
- dm_cdc_errors
- sys.dm_cdc_errors
- sys.dm_cdc_errors_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cdc_errors dynamic management view
- change data capture [SQL Server], error reporting
ms.assetid: 898f2d76-9e63-45ef-94da-8034e86004ab
author: stevestein
ms.author: sstein
ms.openlocfilehash: 506dae205356504c76d47ffe324b82f9f34665f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68018000"
---
# <a name="change-data-capture---sysdm_cdc_errors"></a>Change Data Capture-sys. dm_cdc_errors
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为变更数据捕获日志扫描会话中遇到的每个错误返回一行。  
 
 
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|会话的 ID。<br /><br /> 0 = 在日志扫描会话中未发生错误。|  
|**phase_number**|**int**|表示发生错误时会话所在的阶段的数字。 有关每个阶段的说明，请参阅[transact-sql&#41;&#40;dm_cdc_log_scan_sessions ](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md)。|  
|**entry_time**|**datetime**|记录错误的日期和时间。 此值对应于 SQL 错误日志中的时间戳。|  
|**error_number**|**int**|错误消息的 ID。|  
|**error_severity**|**int**|消息的严重级别，在 1 到 25 之间。|  
|**error_state**|**int**|错误的状态号。|  
|**error_message**|**nvarchar （1024）**|错误的消息正文。|  
|**start_lsn**|**nvarchar （23）**|发生错误时正在处理的行的起始 LSN 值。<br /><br /> 0 = 在日志扫描会话中未发生错误。|  
|**begin_lsn**|**nvarchar （23）**|发生错误时正在处理的事务的起始 LSN 值。<br /><br /> 0 = 在日志扫描会话中未发生错误。|  
|**sequence_value**|**nvarchar （23）**|发生错误时正在处理的行的 LSN 值。<br /><br /> 0 = 在日志扫描会话中未发生错误。|  
  
## <a name="remarks"></a>备注  
 **sys. dm_cdc_errors**包含之前32会话的错误信息。  
  
## <a name="permissions"></a>权限  
 需要 VIEW DATABASE STATE 权限才能查询**sys.databases. dm_cdc_errors**动态管理视图。 有关动态管理视图权限的详细信息，请参阅[&#40;transact-sql&#41;中的动态管理视图和函数](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)。  
  
## <a name="see-also"></a>另请参阅  
 [sys. dm_cdc_log_scan_sessions &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md)   
 [sys. dm_repl_traninfo &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-repl-traninfo-transact-sql.md)  
  
  

