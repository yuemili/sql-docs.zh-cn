---
title: 可滚动游标和事务隔离 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 92e3694690ef1cba210da29766e7528762e691f2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061603"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>可滚动游标和事务隔离
下表列出了控制更改可见性的因素。  
  
|所做的更改：|可见性取决于：|  
|----------------------|----------------------------|  
|游标|游标类型，游标实现|  
|同一事务中的其他语句|游标类型|  
|其他事务中的语句|游标类型，事务隔离级别|  
  
 下图显示了这些因素。  
  
 ![控制更改可见性的因素](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 下表总结了每个游标类型检测自身所做的更改的能力，以及由其自己的事务中的其他操作和其他事务。 后一种更改的可见性取决于游标类型和包含游标的事务的隔离级别。  
  
|Cursor type\action|自己|不同<br /><br /> Txn|其他<br /><br /> Txn<br /><br /> （RU [a]）|其他<br /><br /> Txn<br /><br /> （RC [a]）|其他<br /><br /> Txn<br /><br /> （RR [a]）|其他<br /><br /> Txn<br /><br /> （S [a]）|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|静态|||||||  
|Insert|也许 [b]|否|否|否|否|否|  
|更新|也许 [b]|否|否|否|否|否|  
|删除|也许 [b]|否|否|否|否|否|  
|键集驱动|||||||  
|Insert|也许 [b]|否|否|否|否|否|  
|更新|是|是|是|是|否|否|  
|删除|也许 [b]|是|是|是|否|否|  
|动态|||||||  
|Insert|是|是|是|是|是|否|  
|更新|是|是|是|是|否|否|  
|删除|是|是|是|是|否|否|  
  
 [a] 括号中的字母指示包含游标的事务的隔离级别;其他事务的隔离级别（在其中进行了更改）是不相关的。  
  
 RU：未提交读  
  
 RC：已提交读  
  
 RR：可重复读  
  
 S： Serializable  
  
 [b] 依赖于如何实现游标。 光标是否可以检测到此类更改通过**SQLGetInfo**中的 SQL_STATIC_SENSITIVITY 选项进行报告。
