---
title: 全局设置（日志记录）（OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 12dbcd77-2b90-4fa1-9cf9-239231ea5773
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 374630b5e5eab1602bb33e176e6f205ee1375af9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68264430"
---
# <a name="global-settings-logging-oracletosql"></a>全局设置（日志记录）(OracleToSQL)
使用 "**全局设置**" 对话框指定 SSMA 的日志记录设置。 通常，只能在使用产品支持时更改这些设置。  
  
若要访问此对话框，请在 "**工具**" 菜单上选择 "**全局设置**"，然后单击左窗格底部的 "**日志记录**" 按钮。  
  
## <a name="options"></a>选项  
**消息级别**  
"**消息" 级别**下面有以下选项：  
  
|选项|说明|  
|----------|---------------|  
|**[所有类别]**|用于设置以下所有选项的日志记录级别。|  
|**收集器**|收集有关源架构的元数据并将其保存到项目中。|  
|**转换器**|将源数据库对象（如表和存储过程）的结构转换为相应[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的结构。|  
|**数据迁移**|将源数据库中的数据迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到中。|  
|**格式化**|为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架构生成脚本的转换器的子组件。|  
|**图形用户界面**|使用 SSMA 工具时显示的消息。|  
|**链接器**|解析 SQL 标识符并向其他组件提供信息。|  
|**其他**|所有不在任何其他类别的消息。|  
|**Parser**|分析源架构。|  
|**者**|将源数据库对象加载[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到中。|  
|**TreeConverter**|将源元数据中的对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]转换为元数据。|  
|**测试人员**|使用 SSMA 测试器时显示的消息。|  
  
对于 "**消息级别**" 下的每个选项，请为 SSMA 配置以下日志记录级别之一：  
  
|||  
|-|-|  
|**错误**|仅将严重错误消息写入日志。|  
|**错误**|写入日志的错误消息和严重错误消息。|  
|**警告**|将警告、错误和严重错误消息写入日志。|  
|**信息**|将信息性、警告、错误和严重错误消息写入日志。|  
|**调试**|将所有消息（包括调试消息）写入日志。|  
  
**日志文件路径**  
SSMA 日志文件的文件路径和名称。 若要指定其他名称，请单击当前路径，然后单击浏览（**...**）按钮。  
  
**日志文件大小**  
日志文件的最大大小（KB）。 最小大小为 10 KB。 默认大小为 10240 KB。  
  
**日志文件总数**  
当一个日志填充时，SSMA 将重命名该日志文件并启动一个新日志文件。 通过使用此设置，指定要保留的日志文件的最大数目。 最小值为2。  
  
