---
title: --（注释）(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- --_TSQL
- Comment
- --
dev_langs:
- TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- remarks [SQL Server]
- -- (comment character)
- comments [SQL Server]
ms.assetid: 676ea8c2-52c1-4ef6-9354-320f1a091153
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d7e9aaab99194646874c0823abb61100cdc524aa
ms.sourcegitcommit: 639842f0b70e8c2c9ad5e86f9bfc3a4aad61a1df
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2020
ms.locfileid: "78261696"
---
# <a name="---comment-transact-sql"></a>--（注释）(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  表示用户提供的文本。 可以将注释插入单独行中，嵌套在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令行的结尾或嵌套在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中。 服务器不对注释进行计算。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
-- text_of_comment  
```  
  
## <a name="arguments"></a>参数  
 text_of_comment   
 包含注释文本的字符串。  
  
## <a name="remarks"></a>备注  
将两个连字符 (“--”) 用于单行或嵌套的注释  。 使用 -- 插入的注释通过一个新行终止，该新行由回车符 (u + 000A)、换行符 (u + 000D) 或二者的组合指定  。 注释没有最大长度限制。 下表列出了可用来注释或取消注释文本的键盘快捷键：
  
|操作|Standard|  
|------------|--------------|  
|将选定文本设为注释|Ctrl+K、Ctrl+C|  
|取消注释所选文本|Ctrl+K、Ctrl+U|  
  
 有关键盘快捷方式的详细信息，请参阅 [SQL Server Management Studio 键盘快捷方式](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)。  
  
 有关多行注释的信息，请参阅[斜杠星型（块注释）(Transact-SQL)](../../t-sql/language-elements/slash-star-comment-transact-sql.md)。  
  
## <a name="examples"></a>示例  
 下面的示例使用 -- 注释字符。  
  
```  
-- Choose the AdventureWorks2012 database.  
USE AdventureWorks2012;  
GO  
-- Choose all columns and all rows from the Address table.  
SELECT *  
FROM Person.Address  
ORDER BY PostalCode ASC; -- We do not have to specify ASC because   
-- that is the default.  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [控制流语言 (Transact-SQL)](~/t-sql/language-elements/control-of-flow.md)  
  
  
