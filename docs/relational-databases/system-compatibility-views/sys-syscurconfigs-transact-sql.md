---
title: sys. syscurconfigs （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syscurconfigs
- sys.syscurconfigs_TSQL
- syscurconfigs
- syscurconfigs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.syscurconfigs compatibility view
- syscurconfigs system table
ms.assetid: 454ab849-07a5-4b50-ba0a-6b1b14721f77
author: rothja
ms.author: jroth
ms.openlocfilehash: 1b0fad344831d8073badb2618eb2c34a1cdc2161
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68089182"
---
# <a name="syssyscurconfigs-transact-sql"></a>sys.syscurconfigs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对每个当前配置选项而言都包含一项。 该视图同时还包含四项，用于说明配置结构。 **syscurconfigs**由用户查询时动态生成。 有关详细信息，请参阅[sysconfigures &#40;transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-sysconfigures-transact-sql.md)。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**负值**|**int**|用户可修改的变量值。 仅在执行 RECONFIGURE 后，由[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]使用。|  
|**config.xml**|**smallint**|配置变量号。|  
|**条**|**nvarchar(255)**|对配置选项的解释。|  
|**状态值**|**smallint**|表示选项状态的位图。 可能的值包括：<br /><br /> 0 = 静态。 重新启动服务器后，设置才会生效。<br /><br /> 1 = 动态。 执行 RECONFIGURE 语句后，变量才会生效。<br /><br /> 2 = 高级。 仅当设置了 "**显示高级选项**" 时，才会显示变量。<br /><br /> 3 = 动态和高级。|  
  
## <a name="see-also"></a>另请参阅  
 [将系统表映射到系统视图 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Transact-sql&#41;的兼容性视图 &#40;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
