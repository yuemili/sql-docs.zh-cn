---
title: getDate 方法 (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getDate (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e6b6cfe2-b7c4-4d41-8e09-c68b5086a503
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 12da04a9aa4c3f818960c8683d66e0ca1f1fc31c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67984048"
---
# <a name="getdate-method-int-sqlserverresultset"></a>getDate 方法 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列索引的值作为 Java 编程语言中的 java.sql.Date 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Date getDate(int columnIndex)  
```  
  
#### <a name="parameters"></a>parameters  
 columnIndex  
  
 指示列索引的 int。  
  
## <a name="return-value"></a>返回值  
 Date 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getDate 方法是由 java.sql.ResultSet 接口中的 getDate 方法指定的。  
  
 此方法返回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime 或 smalldatetime 数据类型的有效日期部分，时间部分设置为 Java 时间基线 00:00（午夜）。  
  
## <a name="see-also"></a>另请参阅  
 [getDate 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdate-method-sqlserverresultset.md)   
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
