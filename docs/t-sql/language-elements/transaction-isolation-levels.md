---
title: 事务隔离级别 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], hints
- isolation levels [SQL Server], metadata access
- hints [SQL Server], locking
ms.assetid: 02bb71fa-1e92-4782-a9cf-6e256cc1f3ea
author: rothja
ms.author: jroth
ms.openlocfilehash: 28a8de0654fe6e083b52e83d85653a0d9856d351
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68072201"
---
# <a name="transaction-isolation-levels"></a>事务隔离级别
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不保证通过目录视图、兼容性视图、信息架构视图、元数据发出内置函数访问元数据的查询遵守锁提示。  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]在内部仅按照 READ COMMITTED 隔离级别进行元数据访问。 如果事务有一个隔离级别（例如 SERIALIZABLE），并且您尝试在事务中使用目录视图或元数据发出内置函数访问元数据，则查询将一直运行，直到它们按照 READ COMMITTED 隔离级别完成。 但是，在快照隔离级别下，访问元数据可能会因并发的 DDL 操作而失败。 这是因为未将元数据版本化。 因此，在快照隔离级别下访问下列内容可能会失败：  
  
-   目录视图  
  
-   兼容性视图  
  
-   信息架构视图  
  
-   元数据发出内置函数  
  
-   存储过程的 **sp_help** 组  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 目录过程  
  
-   动态管理视图和函数  
  
 有关隔离级别的详细信息，请参阅 [SET TRANSACTION ISOLATION LEVEL (Transact-SQL)](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)。  
  
 下表概述了各种隔离级别下的元数据访问。  
  
|隔离级别|支持|遵守|  
|---------------------|---------------|-------------|  
|READ UNCOMMITTED|否|不保证|  
|READ COMMITTED|是|是|  
|REPEATABLE READ|否|否|  
|SNAPSHOT ISOLATION|否|否|  
|SERIALIZABLE|否|否|  
  
  
