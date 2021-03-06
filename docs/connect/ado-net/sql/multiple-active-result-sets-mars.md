---
title: 多个活动的结果集 (MARS)
description: 介绍了如何在从单独命令启动 SqlDataReader 的每个实例时，在一个连接上打开多个 SqlDataReader。
ms.date: 08/15/2019
ms.assetid: c90ef863-bac7-44cf-adc1-f05c36fcf57d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 4475e4b8a71b4abcf4e1c2324a49e03a8bb64fbb
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896674"
---
# <a name="multiple-active-result-sets-mars"></a>多个活动的结果集 (MARS)

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

多重活动结果集 (MARS) 是一项可便于在一个连接上执行多个批处理的功能。 在旧版中，一次只能对一个连接执行一个批处理。 使用 MARS 执行多个批处理并不意味着同时执行操作。  
  
## <a name="in-this-section"></a>在本节中  
[启用多重活动结果集](enable-multiple-active-result-sets.md)  
讨论如何在 SQL Server 中使用 MARS。  
  
[操作数据](manipulate-data.md)  
收录了 MARS 应用程序编码示例。  
  
## <a name="related-sections"></a>相关章节  
[异步操作](asynchronous-operations.md)  
详细介绍了如何在 .NET 中使用新的异步功能。  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 和 ADO.NET](index.md)
