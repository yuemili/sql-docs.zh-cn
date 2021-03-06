---
title: sys. xml_schema_types （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_types_TSQL
- xml_schema_types_TSQL
- sys.xml_schema_types
- xml_schema_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_types catalog view
ms.assetid: 441ba49d-f778-4fa1-98c4-ced375a01a34
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a78730509cc1f9eeec83b8d9ff9cb0917e0ed99
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68060429"
---
# <a name="sysxml_schema_types-transact-sql"></a>sys.xml_schema_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为每个 XML 架构组件返回一行，该组件为类型， **Symbol_space** **T**。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**\<继承列>**||从 sys.databases 继承列[xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)。|  
|**is_abstract**|**bit**|1 = 类型是抽象类型。 此类型的元素的所有实例都必须使用**xsi： type**来指示不是抽象的派生类型。<br /><br /> 0 = 类型不是抽象的。 （默认值）|  
|**allows_mixed_content**|**bit**|1 = 允许混合内容<br /><br /> 0 = 不允许混合内容。 （默认值）|  
|**is_extension_blocked**|**bit**|1 = 当**complexType**定义上的 block 特性或上级\<架构> 元素信息项的**blockDefault**属性设置为 "extension" 或 "#all" 时，实例中将阻止具有类型的扩展的替换。<br /><br /> 0 = 不阻塞有扩展名的替换项。|  
|**is_restriction_blocked**|**bit**|1 = 当**complexType**定义上的 block 属性或上级\<架构> 元素信息项的**blockDefault**属性设置为 "限制" 或 "#all" 时，实例中将阻止使用类型的限制进行替换。<br /><br /> 0 = 不阻塞有限制的替换项。 （默认值）|  
|**is_final_extension**|**bit**|1 = 当**complexType**定义中的最终属性或祖先\<架构> 元素信息项的**finalDefault**属性设置为 "extension" 或 "#all" 时，将阻止类型的派生。<br /><br /> 0 = 扩展允许。 （默认值）|  
|**is_final_restriction**|**bit**|1 = 当简单或**complexType**定义中的最终属性或祖先\<架构> 元素信息项的**finalDefault**属性设置为 "限制" 或 "#all" 时，将阻止类型限制的派生。<br /><br /> 0 = 允许限制。 （默认值）|  
|**is_final_list_member**|**bit**|1 = 此简单类型无法用作列表中的项类型。<br /><br /> 0 = 此类型是复杂类型，或者它可以用作列表项类型。 （默认值）|  
|**is_final_union_member**|**bit**|1 = 此简单类型无法用作联合类型的成员类型。<br /><br /> 0 = 此类型是复杂类型， 或者它可以用作联合成员类型。 （默认值）|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 架构 &#40;XML 类型系统&#41; 目录视图 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
