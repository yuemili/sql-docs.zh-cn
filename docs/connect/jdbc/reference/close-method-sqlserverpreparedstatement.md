---
title: close 方法 (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.close
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 36db9ff7-5819-4827-9803-4a81c99069b3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0d8a81004e846986e7352eabb880404ae3cc8c51
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67955595"
---
# <a name="close-method-sqlserverpreparedstatement"></a>close 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  立即释放此 Statement 对象的数据库和 JDBC 资源，而不是等待它们被自动释放。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void close()  
```  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 Close 方法由 java.sql.Statement 接口中的 Close 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
