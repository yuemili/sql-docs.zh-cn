---
title: 使用 SSMA for Access Console （AccessToSQL）入门 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8585ec16-7e0a-483a-b250-adab9b9232a3
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 899070b1405b031e919f50a6d16bc5d6df3adf3e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68222218"
---
# <a name="getting-started-with-ssma-for-access-console-accesstosql"></a>使用 SSMA for Access Console 入门（AccessToSQL）
本部分介绍了启动访问控制台应用程序并开始使用该应用程序的过程。 本文还列出了在典型的 SSMA 控制台输出窗口中使用的约定。  
  
## <a name="launching-ssma-console"></a>启动 SSMA 控制台  
使用以下步骤启动 SSMA 控制台应用程序：  
  
1.  中转到 "**开始**"，然后指向 "**所有程序**"。  
  
2.  单击 "**访问命令提示符**" 快捷方式的 SQL Server 迁移助手。  
  
    它显示 "SSMA 控制台使用情况" `(/? Help)`菜单和，以帮助你开始使用控制台应用程序。  
  
## <a name="procedure-for-using-the-ssma-console"></a>使用 SSMA 控制台的过程  
在 Windows 系统上成功启动控制台后，可以使用以下步骤来处理它：  
  
1.  通过脚本文件配置 SSMA 控制台。 有关此部分的详细信息，请参阅[创建脚本文件 &#40;AccessToSQL&#41;](../../ssma/access/creating-script-files-accesstosql.md)。  
  
2.  [创建变量值文件 &#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
  
3.  [&#40;AccessToSQL 创建服务器连接文件&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
4.  基于你的项目需求[执行 SSMA 控制台 &#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
其他功能：  
  
1.  [指定密码](managing-passwords-accesstosql.md)，并将其导出或导入到其他窗口计算机上  
  
2.  [生成报表](generating-reports-accesstosql.md)以查看详细的 xml 输出报告，以便进行评估/conversion 和数据迁移。 还可以为刷新和同步命令生成详细的错误报告。  
  
## <a name="ssma-console-output-conventions"></a>SSMA 控制台输出约定  
执行 SSMA 脚本命令和选项后，控制台程序会在控制台上向用户显示结果和消息（信息、错误等），或在需要时将其重定向到 xml 输出文件。 输出中的每种消息类型都用一种独特的颜色表示。 例如，以白色表示的短信表示脚本文件命令;绿色颜色表示用户输入的提示，等等。  
  
![SSMA 控制台输出](../../ssma/access/media/ssmaconsoleoutput.jpg "SSMA 控制台输出")  
  
下表中的控制台输出的颜色解释：  
  
|Color|说明|  
|---------|---------------|  
|Red|执行过程中出现错误|  
|灰色|日期和时间戳，向用户发送消息|  
|白色|脚本文件命令，消息类型|  
|独︹|警告|  
|绿色|提示输入用户-输入|  
|蓝|操作的开始、完成和结果|  
  
## <a name="see-also"></a>另请参阅  
[安装访问 SQL Server 迁移助手](installing-sql-server-migration-assistant-for-access-accesstosql.md)  
  
