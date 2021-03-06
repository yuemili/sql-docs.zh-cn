---
title: 配置安全向导：服务帐户
description: 介绍 SQL Server Management Studio 中“配置数据库镜像安全向导”的“服务帐户”页面。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.configdbmsecurwiz.serviceaccounts.f1
ms.assetid: d58d8f93-7888-4d66-af4d-969ef6a2dbee
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8c8a83b68febee5e00a80bd9977713a786b70f9a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "74822451"
---
# <a name="configure-database-mirroring-security-wizard-service-accounts"></a>配置数据库镜像安全向导：服务帐户
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用 Windows 身份验证时，如果服务器实例使用若干个不同的帐户，请为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定服务帐户。 这些服务帐户必须都是域帐户（在相同域或可信域中）。  
  
 如果所有服务器实例都使用同一域帐户或使用基于证书的身份验证，则请将这些字段留空。 只需单击 **“完成”** ，向导将根据当前向导的帐户自动配置帐户。  
  
> [!IMPORTANT]  
>  如果将服务器实例的数据库镜像端点配置为使用证书，您必须将服务帐户字段保留为空。  
  
 **使用 SQL Server Management Studio 配置数据库镜像**  
  
-   [使用 Windows 身份验证建立数据库镜像会话 (SQL Server Management Studio)](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [启动配置数据库镜像安全向导 (SQL Server Management Studio)](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>选项  
 **主体**  
 指定主体服务器实例的服务帐户。 以大写形式输入域名：  
  
 *DOMAINNAME*\\*username*  
  
 **镜像**  
 指定镜像服务器实例的服务帐户。 以大写形式输入域名：  
  
 *DOMAINNAME*\\*username*  
  
 **Witness**  
 指定见证服务器实例的服务帐户。 以大写形式输入域名：  
  
 *DOMAINNAME*\\*username*  
  
## <a name="see-also"></a>另请参阅  
 [数据库属性（“镜像”页）](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [启动数据库镜像监视器 (SQL Server Management Studio)](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [设置数据库镜像或 AlwaysOn 可用性组的登录帐户 (SQL Server)](../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md)  
  
  
