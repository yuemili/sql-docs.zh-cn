---
title: 日期和时间改进（OLE DB） |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
ms.assetid: 71614aaf-0fa4-4fe0-b522-68e2e0b66f43
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1dec9e1281d2ff61dcab9312cdf5a7ad1ecb8da3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62866829"
---
# <a name="date-and-time-improvements-ole-db"></a>日期和时间改进 (OLE DB)
  
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 引入了新的日期和时间数据类型。 本部分介绍如何将这些新类型作为本机客户端[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的扩展公开。 有关对新日期和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时间数据类型的 Native Client 支持的概述，请参阅[日期和时间改进](../native-client/features/date-and-time-improvements.md)。 有关示例，请参阅[使用增强的日期和时间功能 &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md)。  
  
 有关日期和时间数据类型的更多常规信息，请参阅[datetime &#40;transact-sql&#41;](/sql/t-sql/data-types/datetime-transact-sql)。  
  
## <a name="in-this-section"></a>本节内容  
 [针对 OLE DB 日期和时间改进的数据类型支持](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 提供有关支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日期和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时间数据类型 OLE DB （Native Client）类型的信息。  
  
 [OLE DB 的元数据 &#40;&#41;](../../database-engine/dev-guide/metadata-ole-db.md)  
 `ICommandWithParameters::GetParameterInfo`包含有关 DBBINDING 结构、 `ICommandWithParameters::SetParameterInfo` `IColumnsRowset::GetColumnsRowset`、、和 I`ColumnsInfo::GetColumnInfo`的信息。还提供有关 OLE DB 架构行集的更新的信息。  
  
 [绑定和转换 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
 说明在服务器和客户端之间现有和新数据类型的转换规则。  
  
 [&#40;OLE DB 和 ODBC 的增强日期和时间类型的大容量复制&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 描述支持大容量复制操作的日期/时间增强功能。  
  
 [OLE DB API 对日期和时间增强功能的支持](ole-db-api-support-for-date-and-time-enhancements.md)  
 说明支持日期/时间增强功能的 OLE DB API。  
  
 [IRowsetFind 的可比性](../../relational-databases/native-client-ole-db-date-time/comparability-for-irowsetfind.md)  
 说明日期/时间类型和 `IRowsetFind`。  
  
 [旧 SQL Server 版本 &#40;OLE DB 的新日期和时间功能&#41;](new-date-and-time-features-with-previous-sql-server-versions-ole-db.md)  
 说明使用日期和时间增强功能的客户端应用程序与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本通信时的预期行为，以及使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 早期版本编译的客户端向支持日期和时间增强功能的服务器发送命令的预期行为。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client (OLE DB)](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
