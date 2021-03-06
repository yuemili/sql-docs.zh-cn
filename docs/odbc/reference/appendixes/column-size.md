---
title: 列大小 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], column size
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
ms.assetid: 541b83ab-b16d-4714-bcb2-3c3daa9a963b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5639828c90141079ab66f6cceb466328ddb3f56d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019231"
---
# <a name="column-size"></a>列大小
数值数据类型的列（或参数）大小定义为列或参数的数据类型使用的最大位数或数据的精度。 对于字符类型，这是数据的长度（以字符数表示）;对于二进制数据类型，列大小定义为数据的长度（以字节为单位）。 对于时间、时间戳和所有间隔数据类型，这是此数据的字符表示形式中的字符数。 下表显示了为每种简洁的 SQL 数据类型定义的列大小。  
  
|SQL 类型标识符|列大小|  
|-------------------------|-----------------|  
|所有字符类型 [a]，[b]|列或参数的已定义或最大列大小（如 SQL_DESC_LENGTH 描述符字段中包含）。 例如，定义为 CHAR （10）的单字节字符列的列大小为10。|  
|SQL_DECIMAL SQL_NUMERIC|定义的位数。 例如，定义为 NUMERIC （10，3）的列的精度为10。|  
|SQL_BIT [c]|1|  
|SQL_TINYINT [c]|3|  
|SQL_SMALLINT [c]|5|  
|SQL_INTEGER [c]|10|  
|SQL_BIGINT [c]|19（如果已签名）或20（如果未签名）|  
|SQL_REAL [c]|7|  
|SQL_FLOAT [c]|15|  
|SQL_DOUBLE [c]|15|  
|所有二进制类型 [a]，[b]|列或参数的定义的或最大长度（以字节为单位）。 例如，定义为 BINARY （10）的列的长度为10。|  
|SQL_TYPE_DATE [c]|10（ *yyyy-mm-dd*格式的字符数）。|  
|SQL_TYPE_TIME [c]|8（ *hh mm ss*格式的字符数）或 9 + *s* （ *hh： mm： ss*[. fff ...] 格式的字符数，其中*s*是秒的精度）。|  
|SQL_TYPE_TIMESTAMP|16（ *yyyy-mm-dd hh： mm*格式的字符数）<br /><br /> 19（ *yyyy-mm-dd* *hh： mm： ss*格式的字符数）<br /><br /> 或<br /><br /> 20 +*秒*（ *yyyy-mm-dd hh： mm： ss*[. fff ...] 格式的字符数，其中*s*是秒的精度）。|  
|SQL_INTERVAL_SECOND|其中， *p*为间隔的精度， *s*为秒精度， *p* （如果*s*= 0）或*p*+*s*+ 1 （如果*s*>0）。2-d|  
|SQL_INTERVAL_DAY_TO_SECOND|其中， *p*为间隔的精度， *s*为秒精度，9 +*p* （如果*s*= 0）或 10 +*p*+*（如果* *s*>0）。2-d|  
|SQL_INTERVAL_HOUR_TO_SECOND|其中， *p*为间隔的精度， *s*为秒精度，6 +*p* （如果*s*= 0）或 7 +*p*+*s* （如果*s*>0）。2-d|  
|SQL_INTERVAL_MINUTE_TO_SECOND|其中， *p*为间隔的精度， *s*为秒精度，3 +*p* （如果*s*= 0）或 4 +*p*+*s* （如果*s*>0）。2-d|  
|SQL_INTERVAL_YEAR SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p*，其中*p*为间隔的起始精度。2-d|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|3 +*p*，其中*p*是间隔的起始精度。2-d|  
|SQL_INTERVAL_DAY_TO_MINUTE|6 +*p*，其中*p*是间隔的起始精度。2-d|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3 +*p*，其中*p*是间隔的起始精度。2-d|  
|SQL_GUID|36（ *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee*格式的字符数）|  
  
 [a] 对于在 odbc 2.0 驱动程序中调用**SQLSetParam**的 odbc 1.0 应用程序，以及在 odbc 1.0 驱动程序中调用**SQLBindParameter**的 odbc 2.0 应用\*程序，如果为 SQL_LONGVARCHAR 或 SQL_LONGVARBINARY 类型 SQL_DATA_AT_EXEC *StrLen_or_IndPtr* ，则必须将*ColumnSize*设置为要发送的数据的总长度，而不是此表中定义的精度。  
  
 [b] 如果驱动程序无法确定变量类型的列或参数长度，它将返回 SQL_NO_TOTAL。  
  
 [c] 对于此数据类型，将忽略**SQLBindParameter**的*ColumnSize*参数。  
  
 [d] 有关间隔数据类型中列长度的一般规则，请参阅本附录前面的[时间间隔数据类型长度](../../../odbc/reference/appendixes/interval-data-type-length.md)。  
  
 为列（或参数）大小返回的值与任何一个描述符字段中的值都不对应。 值可以来自 SQL_DESC_PRECISION 或 SQL_DESC_LENGTH 字段，具体取决于数据的类型，如下表所示。  
  
|SQL 类型|对应的描述符字段<br /><br /> 列或参数大小|  
|--------------|--------------------------------------------------------------------|  
|所有字符和二进制类型|LENGTH|  
|所有数值类型|PRECISION|  
|所有日期时间和间隔类型|LENGTH|  
|SQL_BIT|LENGTH|
