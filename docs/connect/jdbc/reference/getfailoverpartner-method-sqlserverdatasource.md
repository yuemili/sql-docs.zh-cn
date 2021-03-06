---
title: getFailoverPartner 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getFailoverPartner
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 885f927f-9c48-42e0-a7fb-fd936d2b8130
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b278df5cfa6e3bb80b2b309bf9abf195b249488
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67983255"
---
# <a name="getfailoverpartner-method-sqlserverdatasource"></a>getFailoverPartner 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  返回在数据库镜像配置中使用的故障转移服务器的名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
public string getFailoverPartner()  
```  
  
## <a name="return-value"></a>返回值  
 包含故障转移伙伴名称的字符串  ，如果未设置值，则为 Null。  
  
## <a name="remarks"></a>备注  
 此方法返回的值将反映使用 [setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) 方法设置的故障转移伙伴名称。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDataSource 成员](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 类](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
