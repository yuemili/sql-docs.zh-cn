---
title: isBeforeFirst 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.isBeforeFirst
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e0e2bd28-6949-47dc-b9dd-145ffb337069
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ffe17993b3a03563ec20e8f509e6eae2f6ed47cb
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67977788"
---
# <a name="isbeforefirst-method-sqlserverresultset"></a>isBeforeFirst 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索游标是否位于此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象中的第一行之前。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isBeforeFirst()  
```  
  
## <a name="return-value"></a>返回值  
 如果游标位于第一行之前，则为值 true  。 如果游标位于其他任何位置或结果集不包含任何行，则值为 false  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 isBeforeFirst 方法是由 java.sql.ResultSet 接口中的 isBeforeFirst 方法指定的。  
  
 如果将此方法用于动态游标（包括只进只读游标）且将 selectMethod 连接属性设置为“cursor”，会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
