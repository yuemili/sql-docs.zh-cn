---
title: Microsoft Connector for Oracle | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 92aaf7c04d7a5e176fce4448b9d4f6172b541647
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "75755839"
---
# <a name="microsoft-connector-for-oracle"></a>Microsoft Connector for Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

使用 Microsoft Connector for Oracle，可以从 SSIS 包内的 Oracle 数据源中导出数据，并向其中加载数据。

## <a name="version-support"></a>版本支持

Microsoft Connector for Oracle 支持以下 Microsoft SQL Server 产品：

- SQL Server 2019 及更高版本
- 15.9.3 版本以后的 SQL Server Data Tools (SSDT)

支持以下 Oracle Database 版本的数据源：

- Oracle 10.x
- Oracle 11.x
- Oracle 12c
- Oracle 18c（不支持 Windows 身份验证）

所有操作系统和平台都支持 Oracle Database。
> [!NOTE]
>
> 在 SQL Server 2019 中，Microsoft Connector for Oracle Database 不需要 Oracle 客户端。

## <a name="installation"></a>安装

要为 Oracle 数据库安装连接器，请从 [最新版 Microsoft Connector for Oracle](https://www.microsoft.com/download/details.aspx?id=58228)下载并运行该安装程序。 然后按照安装向导中的说明进行操作。

安装连接器后，必须重启 SQL Server Integration Services，才能确保 Oracle 源和目标正常运行。

要执行面向 SQL Server 2017 及更低版本的 SSIS 包，除了 Microsoft Connector for Oracle，还需要安装 Oracle 客户端以及 Microsoft Connector for Oracle by Attunity，相应版本可见以下链接    ：

- [SQL Server 2017：适用于 Oracle 的 Attunity Microsoft Connector 版本 5.0](https://www.microsoft.com/download/details.aspx?id=55179)
- [SQL Server 2016：适用于 Oracle 的 Attunity Microsoft Connector 版本 4.0](https://www.microsoft.com/download/details.aspx?id=52950)
- [SQL Server 2014：适用于 Oracle 的 Attunity Microsoft Connector 版本 3.0](https://www.microsoft.com/download/details.aspx?id=44582)
- [SQL Server 2012：适用于 Oracle 的 Attunity Microsoft Connector 版本 2.0](https://www.microsoft.com/download/details.aspx?id=29283)

## <a name="uninstallation"></a>卸载

要从 SQL Server 中删除 Microsoft Connector for Oracle Database，可以运行卸载向导。

## <a name="next-steps"></a>后续步骤

- 配置 [Oracle Connection Manager](oracle-connection-manager.md)。
- 配置 [Oracle 源](oracle-source.md)。
- 配置 [Oracle 目标](oracle-destination.md)。
- 若有任何疑问，请访问 [TechCommunity](https://aka.ms/AA5u35j)。
