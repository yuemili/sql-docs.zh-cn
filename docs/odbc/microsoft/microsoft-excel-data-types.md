---
title: Microsoft Excel 数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Excel driver
- Excel data types [ODBC]
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], data types
ms.assetid: 7b44c8e5-0bc3-4912-8a5d-56f4d5562fe6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5a8385c8efb1ab7dcee651e5acb52062292a0bcc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68045025"
---
# <a name="microsoft-excel-data-types"></a>Microsoft Excel 数据类型
下表显示了如何将 Microsoft Excel 驱动程序数据类型映射到 ODBC SQL 数据类型。 Microsoft Excel 驱动程序基于列中的数据，将这些数据类型分配给 Microsoft Excel 表中的列。  
  
|Microsoft Excel 数据类型|ODBC 数据类型|  
|-------------------------------|--------------------|  
|货币|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|LOGICAL|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo**返回 ODBC SQL 数据类型。 对于本主题中前面列出的 ODBC SQL 数据类型，支持*Odbc 程序员参考*的附录 D 中的所有转换。  
  
 下表显示了对 Microsoft Excel 数据类型的限制。  
  
|数据类型|说明|  
|---------------|-----------------|  
|加密数据|Microsoft Excel 驱动程序无法读取加密的数据。|  
|错误字符串|Microsoft Excel 驱动程序无法返回 Microsoft Excel 错误值（#N/A！，#VALUE！，#REF！，#DIV/0！，#NUM！，#NAME？，和 #NULL！）的字符串，但将改为返回 NULL 值。|  
|LOGICAL|逻辑列中的值以0或1的 SQL_C_CHAR 缓冲区形式返回。|  
|NUMBER|如果创建了一个整数列，则可以输入对于整数数据类型太大的数字，并且可以插入包含非整数值的数据，从而使列可以转换为 SQL_DOUBLE。|  
|TEXT|当列中的行包含多个 Microsoft Excel 数据类型时，ODBC Microsoft Excel 驱动程序会将 SQL_VARCHAR 数据类型分配给该列。 有一个例外：如果列仅包含两个或三个日期时间数据类型（日期、时间和日期时间），则 ODBC Microsoft Excel 驱动程序将 SQL_TIMESTAMP 数据类型分配给该列。<br /><br /> 创建零或未指定长度的文本列实际上将返回255字节的列。<br /><br /> 字符串文本可包含任何 ANSI 字符（1-255 decimal）。 使用两个连续的单引号（"）表示一个单引号（'）。<br /><br /> 如果将 NULL 插入到数据类型不是 SQL_VARCHAR 的列，将导致列的数据类型更改为 SQL_VARCHAR。|  
  
 [数据类型限制](../../odbc/microsoft/data-type-limitations.md)中可以找到更多有关数据类型的限制。
