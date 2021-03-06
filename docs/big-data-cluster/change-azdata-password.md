---
title: 更新 AZDATA_PASSWORD
description: 手动更新 `AZDATA_PASSWORD`
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 12/19/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1cc2a7778100be5c919c86a4c949d5aeb784d8e5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "76265989"
---
# <a name="manually-update-azdata_password"></a>手动更新 `AZDATA_PASSWORD`

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

无论群集是否使用 Active Directory 集成运行，都会在部署期间设置 `AZDATA_PASSWORD`。 它为群集控制器和主实例提供了基本身份验证。 本文档介绍了如何手动更新 `AZDATA_PASSWORD`。

## <a name="change-azdata_password-for-controller"></a>更改控制器的 `AZDATA_PASSWORD`

如果群集在非 Active Directory 模式下运行，请执行以下操作来更新 Apache Knox 网关密码：

1. 通过运行以下命令，获取控制器 SQL Server 凭据：

   a. 以 Kubernetes 管理员身份运行以下命令：

   ```bash
   kubectl get secret controller-sa-secret -n <cluster name> -o yaml | grep password
   ```

   b. 对密码执行 Base64 解码：
   
   ```bash
   echo <password from kubectl command>  | base64 --decode && echo
   ```

1. 在单独的命令窗口中，公开控制器数据库服务器端口：

   ```bash
   kubectl port-forward controldb-0 1433:1433 --address 0.0.0.0 -n <cluster name>
   ```
 
1. 使用刚刚获取的系统管理员密码，从 SQL 客户端工具连接到控制器数据库服务器。

1. 为 `AZDATA_USERNAME` 生成新的复杂密码，以替换现有 `AZDATA_PASSWORD`。

   为了简化此示例，后续步骤使用“newPassword”，因为生成的密码是“newPassword”。 

1. 从 users 表获取 `hexsalt`：

   ```sql
   SELECT hexsalt FROM [auth].[users] WHERE username = '<username>'
   ```

   `hexsalt` 返回一个随机十六进制字符串（例如，`64FC59DF31244FFEE02F457BC0750226`）。

1. 使用 `hexsalt` 对新的复杂密码进行加密：

   为了方便起见，我们提供预置工具 `pbkdf2` 来加密此密码。 下载 [`pbkdf2`](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/security/password-hashing/pbkdf2/prebuilt-binaries) 的平台专用 .NET Core 应用。

   此应用是独立式，不需要任何系统必备（如 .NET 运行时）。 若要对密码进行加密，请运行以下命令：

   ```bash
   pbkdf2 <password> <hexsalt>
   J2y4E4dhlgwHOaRr3HKiiVAKBfjuGDyYmzn88VXmrzM=
   ```

1. 更新 users 表中的密码：

   ```SQL
   UPDATE [auth].[users] SET password = 'J2y4E4dhlgwHOaRr3HKiiVAKBfjuGDyYmzn88VXmrzM=' WHERE username = '<username>'
   ```

## <a name="change-azdata_password-in-the-sql-server-master-instance"></a>更改 SQL Server 主实例中的 `AZDATA_PASSWORD`

1. 以任意管理员用户身份连接到主 SQL 终结点。

1. 若要更改在部署期间在参数 `AZDATA_USERNAME` 中定义的登录凭据的密码，请运行以下 TSQL 命令：

   ```sql
   ALTER LOGIN <AZDATA_USERNAME> WITH PASSWORD = 'newPassword'
   ```
