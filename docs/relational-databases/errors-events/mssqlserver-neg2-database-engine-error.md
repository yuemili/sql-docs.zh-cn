---
title: MSSQLSERVER_-2 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "-2"
helpviewer_keywords:
- -2 (Database Engine error)
ms.assetid: f37a7b7d-26e1-4b9e-bcb4-57f7805393d2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 09a5cbc03debdb4fc87986111fb0ac69138715bd
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "67903763"
---
# <a name="mssqlserver_-2"></a>MSSQLSERVER_-2
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|-2|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称||  
|消息正文|超时时间已到。  超时时间在操作完成或服务器没有响应之前已过。 （Microsoft SQL Server，错误: -2）|  
  
## <a name="explanation"></a>说明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端无法连接到服务器。 发生此错误的原因可能是服务器上的防火墙拒绝此连接。  
  
## <a name="user-action"></a>用户操作  
确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务器实例上的防火墙已配置为接受连接。  
  
## <a name="see-also"></a>另请参阅  
[配置 Windows 防火墙以允许 SQL Server 访问](~/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
[为数据库引擎访问配置 Windows 防火墙](~/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
[配置客户端协议](~/database-engine/configure-windows/configure-client-protocols.md)  
[网络协议和网络库](~/sql-server/install/network-protocols-and-network-libraries.md)  
[客户端网络配置](~/database-engine/configure-windows/client-network-configuration.md)  
[配置客户端协议](~/database-engine/configure-windows/configure-client-protocols.md)  
[启用或禁用服务器网络协议](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
