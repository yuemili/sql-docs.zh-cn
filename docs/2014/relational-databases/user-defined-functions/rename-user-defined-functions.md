---
title: 重命名用户定义函数 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: c2695a5c-9cc5-4b18-8771-53027ca9a9af
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3419faca26d9d252610c07cb994ab5faa738f937
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211707"
---
# <a name="rename-user-defined-functions"></a>重命名用户定义函数
  您可以通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 重命名 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的用户定义函数。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要重命名用户定义函数，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   函数名称必须符合 [标识符](../databases/database-identifiers.md)规则。  
  
-   重命名用户定义函数将不会更改 **sys.sql_modules** 目录视图的定义列中相应对象名的名称。 因此，我们建议不要重命名此对象类型。 而是删除存储过程，然后使用新名称重新创建该存储过程。  
  
-   在未将对象更新为反映已对用户定义函数所做的更改时，更改用户定义函数的名称或定义可能导致依赖对象失败。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 权限  
 若要删除函数，要求对函数所属架构具有 ALTER 权限，或对函数具有 CONTROL 权限。 若要重新创建函数，要求在数据库中具有 CREATE FUNCTION 权限，并对创建函数时所在的架构具有 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-rename-user-defined-functions"></a>重命名用户定义函数  
  
1.  在 **“对象资源管理器”** 中，单击包含您要重命名的函数的数据库旁边的加号，然后  
  
2.  单击 **“可编程性”** 文件夹旁的加号。  
  
3.  单击包含要重命名的函数的文件夹旁边的加号：  
  
    -   Table-valued Function  
  
    -   标量值函数  
  
    -   Aggregate 函数  
  
4.  右键单击要重命名的函数，然后选择“重命名”  。  
  
5.  输入函数的新名称。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **重命名用户定义函数**  
  
 无法使用 Transact-SQL 语句执行此任务。 若要使用 Transact-SQL 重命名用户定义函数，必须首先删除现有的函数，然后用新名称重新创建函数。 请确保使用了该函数的旧名称的所有代码和应用程序现在都使用该新名称。  
  
 有关详细信息，请参阅 [CREATE FUNCTION (Transact-SQL)](/sql/t-sql/statements/create-function-transact-sql) 和 [DROP FUNCTION (Transact-SQL)](/sql/t-sql/statements/drop-function-transact-sql)。  
  
## <a name="see-also"></a>另请参阅  
 [sys.sql_expression_dependencies (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)   
 [查看用户定义的函数](user-defined-functions.md)  
  
  
