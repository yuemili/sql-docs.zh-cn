---
title: sp_refreshview （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_refreshview
- sp_refreshview_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_refreshview
ms.assetid: 9ce1d07c-ee66-4a83-8c73-cd2cc104dd08
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3b8c1b95d8d04e2b11982af14971e43e83db146f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68075774"
---
# <a name="sp_refreshview-transact-sql"></a>sp_refreshview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用于更新指定的未绑定到架构的视图的元数据。 由于视图所依赖的基础对象的更改，视图的持久元数据会过期。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_refreshview [ @viewname = ] 'viewname'   
```  
  
## <a name="arguments"></a>参数  
`[ @viewname = ] 'viewname'`视图的名称。 *viewname*的值为**nvarchar**，无默认值。 *viewname*可以是多部分标识符，但只能引用当前数据库中的视图。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或非零数字（失败）  
  
## <a name="remarks"></a>备注  
 如果视图不是使用 schemabinding 创建的，则在对视图的基础对象进行更改时，会影响视图的定义， **sp_refreshview**应运行。 否则，当查询视图时，可能会生成意外结果。  
  
## <a name="permissions"></a>权限  
 要求对视图具有 ALTER 权限，并对视图列引用的公共语言运行时 (CLR) 用户定义类型和 XML 架构集合具有 REFERENCES 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-updating-the-metadata-of-a-view"></a>A. 更新视图的元数据  
 以下示例刷新视图 `Sales.vIndividualCustomer` 的元数据。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sp_refreshview N'Sales.vIndividualCustomer';  
```  
  
### <a name="b-creating-a-script-that-updates-all-views-that-have-dependencies-on-a-changed-object"></a>B. 创建脚本，该脚本可更新与更改对象有依赖关系的所有视图  
 假定表 `Person.Person` 进行了更改，其更改方式影响了基于此表创建的所有视图的定义。 以下示例将创建一个脚本，以便为与表 `Person.Person` 有依赖关系的所有视图刷新源数据。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT DISTINCT 'EXEC sp_refreshview ''' + name + ''''   
FROM sys.objects AS so   
INNER JOIN sys.sql_expression_dependencies AS sed   
    ON so.object_id = sed.referencing_id   
WHERE so.type = 'V' AND sed.referenced_id = OBJECT_ID('Person.Person');  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎存储过程 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.sql_expression_dependencies (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sp_refreshsqlmodule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-refreshsqlmodule-transact-sql.md)  
  
  
