---
title: sys. sysusers （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysusers
- sys.sysusers_TSQL
- sysusers_TSQL
- sysusers
dev_langs:
- TSQL
helpviewer_keywords:
- sysusers system table
- sys.sysusers compatibility view
ms.assetid: 5f0e6a8d-c983-44f6-97e9-aab5bff67d18
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1b8bec28a2e7778a449cb36aeee81481a311c6b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68018060"
---
# <a name="syssysusers-transact-sql"></a>sys.sysusers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  对于数据库中的每[!INCLUDE[msCoName](../../includes/msconame-md.md)]个 windows 用户、windows 组[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、用户或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]角色占一行。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**标识号**|**smallint**|用户 ID，在此数据库中是唯一的。<br /><br /> 1 = 数据库所有者<br /><br /> 如果用户数和角色数超过 32,767，则发生溢出或返回 NULL。|  
|**状态值**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**路径名**|**sysname**|用户名或组名，在此数据库中是唯一的。|  
|**sid**|**varbinary （85）**|此项的安全性标识符。|  
|**作用**|**varbinary （2048）**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**createdate**|**datetime**|帐户的添加日期。|  
|**updatedate**|**datetime**|帐户的上次更改日期。|  
|**altuid**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 如果用户数和角色数超过 32,767，则发生溢出或返回 NULL。|  
|password |**varbinary （256）**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**gid**|**smallint**|此用户所属的组 ID。 如果**uid**与**gid**相同，则此项定义一个组。 如果组和用户的总数超过 32,767，则发生溢出或返回 NULL。|  
|**environ**|**varchar （255）**|保留。|  
|**hasdbaccess**|**int**|1 = 帐户具有数据库访问权。|  
|**islogin**|**int**|1 = 帐户是具有登录帐户的 Windows 组、Windows 用户或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户。|  
|**isntname**|**int**|1 = 帐户是 Windows 组或 Windows 用户。|  
|**isntgroup**|**int**|1 = 帐户是 Windows 组。|  
|**isntuser**|**int**|1 = 帐户是 Windows 用户。|  
|**issqluser**|**int**|1 = 帐户是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户。|  
|**isaliased**|**int**|1 = 帐户化名为另一个用户。|  
|**issqlrole**|**int**|1 = 帐户是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色。|  
|**isapprole**|**int**|1 = 帐户是应用程序角色。|  
  
## <a name="see-also"></a>另请参阅  
 [将系统表映射到系统视图 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Transact-sql&#41;的兼容性视图 &#40;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
