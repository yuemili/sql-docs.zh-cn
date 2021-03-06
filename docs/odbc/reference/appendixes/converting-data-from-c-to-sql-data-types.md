---
title: 将数据从 C 转换为 SQL 数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], about converting
- converting data from c to SQL types [ODBC]
- data conversions from C to SQL types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- SQL data types [ODBC], converting from C types
- data types [ODBC], SQL data types
- data conversions from C to SQL types [ODBC]
- C data types [ODBC], converting to SQL types
ms.assetid: ee0afe78-b58f-4d34-ad9b-616bb23653bd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aca333a6f3006b1f12cf44d1670e38556027e476
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019117"
---
# <a name="converting-data-from-c-to-sql-data-types"></a>将数据从 C 转换为 SQL 数据类型
当应用程序调用**SQLExecute**或**SQLExecDirect**时，驱动程序将从应用程序中的存储位置检索与**SQLBindParameter**绑定的任何参数的数据。 当应用程序调用**SQLSetPos**时，驱动程序将从与**SQLBindCol**绑定的列中检索更新或添加操作的数据。 对于执行时数据参数，应用程序将参数数据与**SQLPutData**一起发送。 必要时，驱动程序将数据从**SQLBindParameter**中的*ValueType*参数指定的数据类型转换为**SQLBindParameter**中*ParameterType*参数指定的数据类型，然后将数据发送到数据源。  
  
 下表显示了从 ODBC C 数据类型到 ODBC SQL 数据类型的支持转换。 实心圆圈表示 SQL 数据类型的默认转换（在 SQL_C_DEFAULT *ValueType*值或 SQL_DESC_CONCISE_TYPE 描述符字段时，数据将转换为 C 数据类型）。 空心圆表示支持的转换。  
  
 转换后的数据的格式不受 Windows®的 "国家/地区" 设置的影响。  
  
 ![支持的转换：从 ODBC C 到 SQL 数据类型](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 以下各节中的表描述了驱动程序或数据源如何转换发送到数据源的数据;驱动程序需要支持从所有 ODBC C 数据类型到它们支持的 ODBC SQL 数据类型的转换。 对于给定的 ODBC C 数据类型，表的第一列列出了**SQLBindParameter**中*ParameterType*参数的合法输入值。 第二列列出驱动程序执行的测试结果，以确定是否可以转换数据。 第三列列出了**SQLExecDirect**、 **SQLExecute**、 **SQLBulkOperations**、 **SQLSetPos**或**SQLPutData**为每个结果返回的 SQLSTATE。 仅当返回 SQL_SUCCESS 时才将数据发送到数据源。  
  
 如果**SQLBindParameter**中的*ParameterType*参数包含的 ODBC SQL 数据类型的标识符不显示在给定 C 数据类型的表中，则**SQLBindParameter**将返回 SQLSTATE 07006 （受限制的数据类型属性冲突）。 如果*ParameterType*参数包含特定于驱动程序的标识符，并且该驱动程序不支持从特定 ODBC C 数据类型到该驱动程序特定的 SQL 数据类型的转换，则**SQLBINDPARAMETER**将返回 SQLSTATE HYC00 （未实现可选功能）。  
  
 如果在**SQLBindParameter**中指定的*ParameterValuePtr*和*StrLen_or_IndPtr*参数均为 null 指针，则该函数将返回 SQLSTATE HY009 （null 指针的使用无效）。 尽管表中没有显示，但应用程序会将**SQLBindParameter**参数*StrLen_or_IndPtr*的长度/指示器*StrLen_or_IndPtr*缓冲区的值或**SQLPutData**的参数值设置为 SQL_NULL_DATA，以指定 NULL SQL 数据值。 （ *StrLen_or_IndPtr*参数对应于 APD 的 SQL_DESC_OCTET_LENGTH_PTR 字段。）应用程序将\*这些值设置为 SQL_NTS 以指定**SQLPutData**中**SQLBindParameter**或\* *DataPtr*的*ParameterValuePtr*中的值（由 APD 的 SQL_DESC_DATA_PTR 字段指向）为以 null 值结束的字符串。  
  
 表中使用了以下术语：  
  
-   **数据的字节长度**-可发送到数据源的 SQL 数据的字节数，数据在发送到数据源之前是否会被截断。 对于字符串数据，这不包括 null 终止字符的空间。  
  
-   **列字节长度**-在数据源中存储数据所需的字节数。  
  
-   **字符字节长度**-以字符形式显示数据所需的最大字节数。 这是针对[显示大小](../../../odbc/reference/appendixes/display-size.md)中的每个 SQL 数据类型定义的，但字符字节长度不以字节为单位，而显示大小为字符。  
  
-   **位数**-用于表示数字的字符数，包括减号、小数点和指数（如果需要）。  
  
-   **字词**   
     ***斜体***-SQL 语法的元素。 有关语法元素的语法，请参阅 "[附录 C： SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)"。  
  
 本部分包含下列主题。  
  
-   [从 C 到 SQL：字符](../../../odbc/reference/appendixes/c-to-sql-character.md)  
  
-   [从 C 到 SQL：数字](../../../odbc/reference/appendixes/c-to-sql-numeric.md)  
  
-   [从 C 到 SQL：位](../../../odbc/reference/appendixes/c-to-sql-bit.md)  
  
-   [从 C 到 SQL：二进制](../../../odbc/reference/appendixes/c-to-sql-binary.md)  
  
-   [从 C 到 SQL：日期](../../../odbc/reference/appendixes/c-to-sql-date.md)  
  
-   [从 C 到 SQL：GUID](../../../odbc/reference/appendixes/c-to-sql-guid.md)  
  
-   [从 C 到 SQL：时间](../../../odbc/reference/appendixes/c-to-sql-time.md)  
  
-   [从 C 到 SQL：时间戳](../../../odbc/reference/appendixes/c-to-sql-timestamp.md)  
  
-   [从 C 到 SQL：年月间隔](../../../odbc/reference/appendixes/c-to-sql-year-month-intervals.md)  
  
-   [从 C 到 SQL：日期时间间隔](../../../odbc/reference/appendixes/c-to-sql-day-time-intervals.md)  
  
-   [从 C 到 SQL 的数据转换示例](../../../odbc/reference/appendixes/c-to-sql-data-conversion-examples.md)
