---
title: SQLConnect |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLConnect function
ms.assetid: 6da74e3a-4388-4907-81cb-987389bae467
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d5292d3141d6ae520a333827796ca8fc6005be15
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63067655"
---
# <a name="sqlconnect"></a>SQLConnect
  当打开连接时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 将 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 和 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 设置为用于打开此连接的身份验证方法。 有关 Spn 的详细信息，请参阅[&#40;ODBC&#41;的客户端连接中的服务主体名称 &#40;spn&#41; ](../native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)。  
  
## <a name="sqlconnect-support-for-high-availability-disaster-recovery"></a>对高可用性、灾难恢复的 SQLConnect 支持  
 有关使用**SQLConnect**连接到[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]群集的详细信息，请参阅[高可用性和灾难恢复的 SQL Server Native Client 支持](../native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLConnect 函数](https://go.microsoft.com/fwlink/?LinkId=101541)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
