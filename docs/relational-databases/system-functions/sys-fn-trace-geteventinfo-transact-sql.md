---
title: sys. fn_trace_geteventinfo （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_trace_geteventinfo
- fn_trace_geteventinfo_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- events [SQL Server], status information
- fn_trace_geteventinfo function
- sys.fn_trace_geteventinfo function
- status information [SQL Server], events
ms.assetid: 5b1c858a-ca43-4e2b-9d67-8654daaf0cc5
author: rothja
ms.author: jroth
ms.openlocfilehash: 62296eb8d1ef53969e33f3807bd81f47025a4893
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68059281"
---
# <a name="sysfn_trace_geteventinfo-transact-sql"></a>sys.fn_trace_geteventinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关所跟踪的事件的信息。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 请改用扩展事件。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
fn_trace_geteventinfo ( trace_id )  
```  
  
## <a name="arguments"></a>参数  
 *trace_id*  
 跟踪的 ID。 *trace_id*为**int**，没有默认值。  
  
## <a name="tables-returned"></a>返回的表  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**eventid**|**int**|所跟踪的事件的 ID|  
|**columnid**|**int**|为每个事件收集的所有列的 ID 号|  
  
## <a name="remarks"></a>备注  
 当传递特定跟踪的 ID 时， **fn_trace_geteventinfo**返回有关该跟踪的信息。 传递无效 ID 时，此函数将返回空行集。  
  
## <a name="permissions"></a>权限  
 要求对服务器具有 ALTER TRACE 权限。  
  
## <a name="examples"></a>示例  
 以下示例返回有关编号为 2 的跟踪的信息。  
  
```  
SELECT * FROM fn_trace_geteventinfo(2) ;  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_trace_setevent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [创建跟踪 (Transact-SQL)](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [sp_trace_create (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [sp_trace_generateevent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setstatus (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [sys.fn_trace_getinfo (Transact-SQL)](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [sys. fn_trace_gettable &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)   
 [sys.fn_trace_getfilterinfo (Transact-SQL)](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)  
  
  
