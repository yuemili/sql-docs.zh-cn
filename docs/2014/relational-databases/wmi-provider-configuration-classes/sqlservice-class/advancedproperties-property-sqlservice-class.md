---
title: AdvancedProperties 属性（SqlService 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- AdvancedProperties Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- AdvancedProperties property
ms.assetid: 63bcb7e2-1f78-4961-b4b9-1b635a89079b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: abe9d977dfcde5523e875881b1a5b80be7b1b887
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63223220"
---
# <a name="advancedproperties-property-sqlservice-class"></a>AdvancedProperties 属性（SqlService 类）
  获取一组包含 `SqlService` 对象的高级属性的对象引用。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.AdvancedProperties [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 一个表示服务的 [SqlService 类](sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 包含`SqlService`对象的高级属性的[SqlServiceAdvancedProperty 类](../sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md)对象的数组。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
