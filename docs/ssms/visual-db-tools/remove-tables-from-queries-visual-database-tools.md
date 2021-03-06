---
title: 从查询删除表
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting tables
- removing tables
- dropping tables
- queries [SQL Server], tables
ms.assetid: 8fea0b4f-99b7-4050-8d6f-a97ffb839619
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 32c25c3ded07e84e436b69af5baac5634909998c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75255251"
---
# <a name="remove-tables-from-queries-visual-database-tools"></a>从查询中删除表 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
可从查询中移除表或任何表值对象。  
  
> [!NOTE]  
> 移除表或表值对象不会从数据库中删除任何内容，该操作只会将表或表值对象从当前查询中移除。 若要详细了解如何从数据库中删除表，请参阅[操作说明：从数据库中删除表 https://msdn.microsoft.com/ca6aa3e9-9885-44c3-bafc-aec441fd97ec) 。  
  
### <a name="to-remove-a-table-or-table-structured-object"></a>移除表或表结构对象  
  
-   在“关系图”  窗格中，选择表、视图、用户定义函数、同义词或查询，再按 Delete；或者右键单击该对象，然后在显示的对话框中选择“删除”  。 您可一次选择和移除多个对象。  
  
    -或-  
  
-   在 **SQL 窗格**中删除对该对象的所有引用。  
  
当移除表或表值对象时，查询和视图设计器将自动删除涉及该表或表值对象的联接，并在“SQL 窗格”  和“条件窗格”  中删除对该对象的列的引用。 但是，如果查询包含涉及该对象的复杂表达式，则只有在移除对该对象的所有引用后才会自动移除该对象。  
  
## <a name="see-also"></a>另请参阅  
[向查询添加表](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md)  
[创建表别名](../../ssms/visual-db-tools/create-table-aliases-visual-database-tools.md)  
[指定搜索条件](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[汇总查询结果](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[对查询执行基本操作](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
