---
title: sys. event_notifications （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- event_notifications_TSQL
- event_notifications
- sys.event_notifications_TSQL
- sys.event_notifications
dev_langs:
- TSQL
helpviewer_keywords:
- sys.event_notifications catalog view
ms.assetid: 136a76ee-2b35-4418-ab46-fda2d51f7d99
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 736083db5043dd8bcb9dce9f828a9191c582c872
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68048417"
---
# <a name="sysevent_notifications-transact-sql"></a>sys.event_notifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  为事件通知的每个对象都返回一行，其中**sys. type** = EN。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**路径名**|**sysname**|事件通知的名称。|  
|**object_id**|**int**|对象标识号。 在数据库中是唯一的。|  
|**parent_class**|**tinyint**|父级的类。<br /><br /> 0 = 数据库<br /><br /> 1 = 对象或列|  
|**parent_class_desc**|**nvarchar （60）**|DATABASE<br /><br /> OBJECT_OR_COLUMN|  
|**parent_id**|**int**|父对象的非零 ID。<br /><br /> 0 = 父类是数据库。|  
|**create_date**|**datetime**|创建日期。|  
|**modify_date**|**datetime**|始终等于**create_date**。|  
|service_name |**nvarchar(256)**|向其发送通知的目标服务的名称。|  
|**broker_instance**|**nvarchar(128)**|向其发送通知的 Broker 实例。|  
|**principal_id**|**int**|拥有此事件通知的数据库主体的 ID。|  
|**creator_sid**|**varbinary （85）**|创建事件通知的登录的 SID。<br /><br /> 如果未指定 FAN_IN 选项，则为 NULL。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;的对象目录视图](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
