---
title: 故障排除
description: 为已知问题的解决提供一个起点。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c9be3a8dff314f6645029fb54803ad30dc04db27
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727565"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>SQL Server 中的机器学习故障排除
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

将本文作为解决已知问题的起点。

## <a name="known-issues"></a>已知问题

以下文章介绍了当前版本和以前版本的已知问题：

+ [R Services 的已知问题](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [SQL Server 2016 发行说明](../sql-server/sql-server-2016-release-notes.md)
+ [SQL Server 2017 发行说明](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>如何收集系统信息

如果遇到错误或者需要了解环境中出现的问题，请务必系统地收集相关信息。 下面的文章提供了有助于进行自助故障排除或请求技术支持的信息列表。

+ [收集数据进行机器学习故障排除](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>安装和配置指南

如果尚未使用 SQL Server 设置机器学习，或者要添加此功能，请从此处开始：

+ [安装 SQL Server 机器学习服务（数据库内）](install/sql-machine-learning-services-windows-install.md)
+ [安装 SQL Server Machine Learning Server（独立版）](install/sql-machine-learning-standalone-windows-install.md)
+ [命令提示符设置](install/sql-ml-component-commandline-install.md)
+ [脱机设置（无 Internet）](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>配置

以下文章包含有关默认值以及如何为实例上的机器学习自定义配置的信息：

+ [在 SQL Server 机器学习服务中缩放外部脚本的并发执行](administration/modify-user-account-pool.md)   
+ [配置和管理高级分析扩展](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [如何创建资源池](r/how-to-create-a-resource-pool-for-r.md)
+ [R 工作负荷优化](r/operationalizing-your-r-code.md)
