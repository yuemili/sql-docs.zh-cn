---
title: onError 事件（RDS） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- onError event [ADO]
ms.assetid: b01cbc62-fbd7-4068-b16c-8b0f80a05887
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9f6a1a532b092acb6c23faf4282d40100cc579c6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67963846"
---
# <a name="onerror-event-rds"></a>onError 事件 (RDS)
只要在操作过程中发生错误，就会调用**onError**事件。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
  
```  
  
onError SCode, Description, Source, CancelDisplay  
```  
  
#### <a name="parameters"></a>parameters  
 *SCode*  
 一个整数，指示错误的状态代码。  
  
 *说明*  
 指示错误说明的**字符串**。  
  
 *数据源*  
 一个**字符串**，指示导致错误的查询或命令。  
  
 *CancelDisplay*  
 一个**布尔**值，如果设置为**True**，则将阻止错误显示在对话框中。  
  
## <a name="applies-to"></a>应用于  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件模型示例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)


