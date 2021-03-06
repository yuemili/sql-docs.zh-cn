---
title: 在 Linux 上安装 SQL Server 机器学习服务（Python、R）
description: 了解如何在 Linux 上安装 SQL Server 机器学习服务（Python 和 R）：Red Hat、Ubuntu 和 SUSE。
author: dphansen
ms.author: davidph
ms.reviewer: vanto
manager: cgronlun
ms.date: 02/03/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 71ab699e99a3d22b6b04299b8de1ccb18e5f0708
ms.sourcegitcommit: 1b0906979db5a276b222f86ea6fdbe638e6c9719
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2020
ms.locfileid: "76971374"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-linux"></a>在 Linux 上安装 SQL Server 机器学习服务（Python 和 R）

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何在 Linux 上安装 [SQL Server 机器学习服务](../advanced-analytics/index.yml)。 可使用机器学习服务在数据库中执行 Python 和 R 脚本。

支持以下 Linux 分发版：

- Red Hat Enterprise Linux (RHEL)
- SUSE Linux Enterprise Server (SLES)
- Ubuntu

机器学习服务是数据库引擎的一项附加功能。 虽然可以[同时安装数据库引擎和机器学习服务](#install-all)，但最好先安装并配置 SQL Server 数据库引擎，以便在添加更多组件之前解决所有问题。 

Python 和 R 扩展的包位于 SQL Server Linux 源存储库中。 如果已为数据库引擎安装配置了源存储库，则可以使用相同的存储库注册运行 mssql-mlservices 包安装命令  。

Linux 容器也支持机器学习服务。 我们不提供带有机器学习服务的预构建容器，但你可以使用 [GitHub 中的示例模板](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices)在 SQL Server 容器中创建一个容器。

机器学习服务默认安装在 SQL Server 大数据群集上，用户无需按照此示例中的步骤执行操作。 有关详细信息，请参阅[在大数据群集上使用机器学习服务（Python 和 R）](../big-data-cluster/machine-learning-services.md)。

## <a name="uninstall-preview-release"></a>卸载预览版

如果安装了预览版本（社区技术预览版 (CTP) 或候选发布），建议先卸载此版本以删除以前的所有包，然后再安装 SQL Server 2019。 不支持并行安装多个版本，并且包列表在最后几个预览版 (CTP/RC) 中进行了更改。

### <a name="1-confirm-package-installation"></a>1.确认包安装

首先可能需要检查是否存在以前的安装。 以下文件指示现有安装：checkinstallextensibility.sh、exthost、launchpad。

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-ctprc-packages"></a>2.卸载 CTP/RC 包

在最低包级别进行卸载。 依赖于较低级别包的所有上游包都会自动卸载。

  + 对于 R 集成，请删除 **microsoft-r-open***
  + 对于 Python 集成，请删除 **mssql-mlservices-python**

下表显示了用于删除包的命令。

| 平台  | 包删除命令 | 
|-----------|----------------------------|
| Red Hat   | `sudo yum remove microsoft-r-open-mro-3.4.4`<br/>`sudo yum remove msssql-mlservices-python` |
| SUSE  | `sudo zypper remove microsoft-r-open-mro-3.4.4`<br/>`sudo zypper remove msssql-mlservices-python` |
| Ubuntu    | `sudo apt-get remove microsoft-r-open-mro-3.4.4`<br/>`sudo apt-get remove msssql-mlservices-python`|

> [!Note]
> Microsoft R Open 3.4.4 由两个包组成，具体取决于之前安装的 CTP 版本。 （foreachiterators 包已合并到 CTP 2.2 中的主 mro 包中。）如果在删除 microsoft-r-open-mro-3.4.4 后，这些包中的任何包仍然存在，则应单独删除它们。
> ```
> microsoft-r-open-foreachiterators-3.4.4
> microsoft-r-open-mkl-3.4.4
> microsoft-r-open-mro-3.4.4
> ```

### <a name="3-proceed-with-install"></a>3.继续安装

使用本文中针对操作系统的说明在最高包级别进行安装。

对于每组特定于操作系统的安装说明，*最高包级别*为**示例 1 - 完全安装**（一组完整的包）或**示例 2 - 最小安装**（可行安装所需的最少包数）。

1. 对于 R 集成，请从 [MRO](#mro) 开始，因为它是必备组件。 如果没有该组件，则无法安装 R 集成。

2. 使用操作系统的包管理器和语法运行安装命令： 

   + [Red Hat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>必备条件

+ Linux 版本必须[受 SQL Server 支持](sql-server-linux-release-notes-2019.md#supported-platforms)，但不包括 Docker 引擎。 受支持的版本包括：

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ （仅限 R）[Microsoft R Open](#mro) 为 SQL Server 中的 R 功能提供基本 R 发行版

+ 应安装用于运行 T-SQL 命令的工具。 需要使用查询编辑器进行安装后配置和验证。 我们建议使用 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux)，它是在 Linux 上运行的免费下载。

<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>Microsoft R Open (MRO) 安装

要使用通过机器学习服务安装的 RevoScaleR、MicrosoftML 和其他 R 包，Microsoft 的 R 基础发行版是先决条件。

所需版本为 MRO 3.5.2。

从以下两种安装 MRO 的方法中进行选择：

+ 从 MRAN 下载 MRO tarball，解压缩并运行其 install.sh 脚本。 如果要使用此方法，可以按照 [MRAN 上的安装说明](https://mran.microsoft.com/releases/3.5.2)进行操作。

+ 或者，如下所述注册 **packages.microsoft.com** 存储库以安装包含 MRO 发行版的两个软件包：microsoft-r-open-mro 和 microsoft-r-open-mkl。 

以下命令可注册提供 MRO 的存储库。 注册后，用于安装其他 R 包的命令（如 mssql-mlservices-mml-r）将自动包含作为包依赖项的 MRO。

#### <a name="mro-on-ubuntu"></a>Ubuntu 上的 MRO

```bash
# Install as root
sudo su

# Optionally, if your system does not have the https apt transport option
apt-get install apt-transport-https

# Set the location of the package repo the "prod" directory containing the distribution.
# This example specifies 16.04. Replace with 14.04 if you want that version
wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the repo
dpkg -i packages-microsoft-prod.deb

# Update packages on your system (required), including MRO installation
sudo apt-get update
```

#### <a name="mro-on-red-hat"></a>Red Hat 上的 MRO

```bash
# Import the Microsoft repository key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc


# Set the location of the package repo at the "prod" directory
# The following command is for version 7.x
# For 6.x, replace 7 with 6 to get that version
rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm

# Update packages on your system (optional)
yum update
```

#### <a name="mro-on-suse"></a>SUSE 上的 MRO

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SUSE in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system (optional)
zypper update
```

## <a name="package-list"></a>包列表

在已连接 Internet 的设备上，将使用针对每个操作系统的包安装程序独立于数据库引擎下载和安装相应的包。 下表介绍了所有可用包，但对于 R 和 Python，需要指定提供完整功能安装或最小功能安装的包。

| 包名称 | 适用对象 | 说明 |
|--------------|----------|-------------|
|mssql-server-extensibility  | All | 用于运行 R 和 Python 代码的可扩展性框架。 |
| microsoft-openmpi  | Python、R | Revo* 库在 Linux 上进行并行化所使用的消息传递接口。 |
| mssql-mlservices-python | Python | Anaconda 和 Python 的开放源代码发行版。 |
|mssql-mlservices-mlm-py  | Python | 完全安装  。 提供用于图像特征化和文本情绪分析的 revoscalepy、microsoftml、预先训练的模型。| 
|mssql-mlservices-packages-py  | Python | 最小安装  。 提供 revoscalepy 和 microsoftml。 <br/>不包括预先训练的模型。 | 
| [microsoft-r-open*](#mro) | R | 由三个包组成的 R 的开放源代码发行版。 |
|mssql-mlservices-mlm-r  | R | 完全安装  。 提供用于图像特征化和文本情绪分析的 RevoScaleR、MicrosoftML、sqlRUtils、olapR、预先训练的模型。| 
|mssql-mlservices-packages-r  | R | 最小安装  。 提供 RevoScaleR、sqlRUtils、MicrosoftML、olapR。 <br/>不包括预先训练的模型。 | 

<a name="RHEL"></a>

## <a name="redhat-commands"></a>RedHat 命令

可以安装所需的任何语言支持组合（一种或多种语言）。 对于 R 和 Python，有两个包可供选择。 其中一个包提供所有可用功能，其特征为完全安装  。 替代选项不包括预先训练的机器学习模型，被认为是最小安装  。

> [!Tip]
> 如果可以，请在安装之前运行 `yum clean all` 以刷新系统中的包。

### <a name="example-1----full-installation"></a>示例 1 - 完全安装 

包括开放源代码 R 和 Python、扩展性框架、microsoft-openmpi、扩展（R、Python）以及机器学习库和 R 和 Python 的预先训练模型。 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.7*
sudo yum install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>示例 2 - 最小安装 

包括开放源代码 R 和 Python、扩展性框架、microsoft-openmpi、核心 Revo * 库以及 R 和 Python 的机器学习库。 不包括预先训练的模型。

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.7*
sudo yum install mssql-mlservices-packages-r-9.4.7*
```

<a name="ubuntu"></a>

## <a name="ubuntu-commands"></a>Ubuntu 命令

可以安装所需的任何语言支持组合（一种或多种语言）。 对于 R 和 Python，有两个包可供选择。 其中一个包提供所有可用功能，其特征为完全安装  。 替代选项不包括预先训练的机器学习模型，被认为是最小安装  。

> [!Tip]
> 如果可以，请在安装之前运行 `apt-get update` 以刷新系统中的包。 此外，Ubuntu 的一些 docker 映像可能没有 https apt 传输选项。 若要进行安装，请使用 `apt-get install apt-transport-https`。

### <a name="example-1----full-installation"></a>示例 1 - 完全安装 

包括开放源代码 R 和 Python、扩展性框架、microsoft-openmpi、扩展（R、Python）以及机器学习库和 R 和 Python 的预先训练模型。 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
```

### <a name="example-2---minimum-installation"></a>示例 2 - 最小安装 

包括开放源代码 R 和 Python、扩展性框架、microsoft-openmpi、核心 Revo * 库以及 R 和 Python 的机器学习库。 不包括预先训练的模型。 

```bash
# Install as root or sudo
# Minimum install of R, Python
# No aasterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
```

<a name="suse"></a>

## <a name="suse-commands"></a>SUSE 命令

可以安装所需的任何语言支持组合（一种或多种语言）。 对于 R 和 Python，有两个包可供选择。 其中一个包提供所有可用功能，其特征为完全安装  。 替代选项不包括预先训练的机器学习模型，被认为是最小安装  。

### <a name="example-1----full-installation"></a>示例 1 - 完全安装 

包括开放源代码 R 和 Python、扩展性框架、microsoft-openmpi、扩展（R、Python）以及机器学习库和 R 和 Python 的预先训练模型。 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.7*
sudo zypper install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>示例 2 - 最小安装 

包括开放源代码 R 和 Python、扩展性框架、microsoft-openmpi、核心 Revo * 库以及 R 和 Python 的机器学习库。 不包括预先训练的模型。 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.7*
sudo zypper install mssql-mlservices-packages-r-9.4.7*
```

## <a name="post-install-config-required"></a>安装后配置（必需）

其他配置主要通过 [mssql-conf 工具](sql-server-linux-configure-mssql-conf.md)完成。


1. 添加用于运行 SQL Server 服务的 mssql 用户帐户。 如果之前未运行过该安装程序，则必须这样做。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. 接受开放源代码 R 和 Python 的许可协议。 可以通过多种方式来完成此项工作。 如果之前已接受 SQL Server 许可并且现将添加 R 或 Python 扩展，则以下命令可表示你同意其条款：

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```

   另一种工作流是，如果未接受过 SQL Server 数据库引擎许可协议，则在运行 `mssql-conf setup` 时，安装程序会检测 mssql-mlservices 包，并提示你接受 EULA。 有关 EULA 参数的详细信息，请参阅[使用 mssql-conf 工具配置 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-eula)。

3. 启用出站网络访问。 默认情况下，出站网络访问处于禁用状态。 若要启用出站请求，请使用 mssql-conf 工具设置“outboundnetworkaccess”布尔属性。 有关详细信息，请参阅[使用 mssql-conf 配置 Linux 上的 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)。

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. （仅适用于 R 功能集成）请设置“MKL_CBWR”环境变量，以确保从 Intel 数学核心函数库 (MKL) 计算得到[一致的输出结果](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)  。

   + 在用户主目录中编辑或创建名为 .bash_profile 的文件，并将行 `export MKL_CBWR="AUTO"` 添加到该文件中  。

   + 通过在 bash 命令提示符处键入 `source .bash_profile` 来执行此文件。

5. 重启 SQL Server Launchpad 服务和数据库引擎实例，以从 INI 文件中读取更新后的值。 每当修改与扩展性相关的设置时，都会收到重启消息提醒。  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

6. 使用 Azure Data Studio 或使用运行 Transact-SQL 的其他工具（如 SQL Server Management Studio，仅限 Windows）来启用外部脚本执行。 

   ```bash
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. 再次重启 Launchpad 服务。

## <a name="verify-installation"></a>验证安装

可在 `/opt/mssql/mlservices/libraries/RServer` 中找到 R 库（MicrosoftML、RevoScaleR 及其他库）。

可在 `/opt/mssql/mlservices/libraries/PythonServer` 中找到 Python 库（microsoftml 和 revoscalepy）。

若要验证安装，请运行可执行调用 R 或 Python 的系统存储过程的 T-SQL 脚本。 需要使用查询工具来完成此任务。 Azure Data Studio 就是不错的选择。 其他常用工具（如 SQL Server Management Studio 或 PowerShell）仅适用于 Windows。 如果 Windows 计算机上安装了这些工具，请使用其连接到数据库引擎的 Linux 安装。

请执行以下 SQL 命令以测试 SQL Server 中的 R 执行。 如果脚本未运行，则尝试重启服务，`sudo systemctl restart mssql-server.service`。

```r
EXEC sp_execute_external_script   
@language =N'R', 
@script=N' 
OutputDataSet <- InputDataSet', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```
 
请执行以下 SQL 命令以测试 SQL Server 中的 Python 执行。 
 
```python
EXEC sp_execute_external_script  
@language =N'Python', 
@script=N' 
OutputDataSet = InputDataSet; 
', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```

<a name="install-all"></a>

## <a name="chained-combo-install"></a>链式“组合”安装

通过在安装数据库引擎的命令上附加 R 或 Python 包和参数，可在一个过程中安装和配置数据库引擎和机器学习服务。 

1. 对于 R 集成，请安装 [Microsoft R Open](#mro)，将其作为必备组件。 如果没有安装 R 功能，请跳过此步骤。

2. 提供包含数据库引擎的命令行以及语言扩展功能。

  可以将单项功能（如 Python 集成）添加到数据库引擎安装中。

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* 
  ```

  或者，同时添加两项扩展（R、Python）。

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* mssql-mlservices-packages-py-9.4.7*
  ```

3. 接受许可协议并完成安装后配置。 使用 **mssql-conf** 工具完成此任务。

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  系统将提示接受数据库引擎的许可协议、选择版本以及设置管理员密码。 系统还会提示你接受机器学习服务的许可协议。

4. 如果系统出现重启提示，请重启服务。

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>无人参与的安装

对数据库引擎使用[无人参与安装](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended)，添加 mssql-mlservices 和 EULA 的包。

回想一下，安装程序或 mssql-conf 工具会提示接受许可协议。 如果已配置 SQL Server 数据库引擎且已接受其 EULA，请使用开放源代码 R 和 Python 发行版的某个特定于 mlservices 的 EULA 参数：

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

EULA 接受的所有可能的排列方式都记录在[使用 mssql-conf 工具配置 Linux 上的 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-eula) 中。

## <a name="offline-installation"></a>脱机安装

有关安装包的步骤，请按照[脱机安装](sql-server-linux-setup.md#offline)说明进行操作。 找到下载网站，然后使用下面的包列表下载特定的包。

> [!Tip]
> 一些包管理工具提供可帮助确定包依赖项的命令。 对于 yum，请使用 `sudo yum deplist [package]`。 对于 Ubuntu，请在使用 `sudo apt-get install --reinstall --download-only [package name]` 之后使用 `dpkg -I [package name].deb`。


#### <a name="download-site"></a>下载站点

可以从 [https://packages.microsoft.com/](https://packages.microsoft.com/) 下载包。 R 和 Python 的所有 mlservices 包都与数据库引擎包位于相同位置。 mlservices 包的基础版本为 9.4.6。 回想一下，microsoft-r-open 包位于[其他存储库](#mro)中。

#### <a name="rhel7-paths"></a>RHEL/7 路径

|||
|--|----|
| mssql/mlservices 包 | [https://packages.microsoft.com/rhel/7/mssql-server-2019/](https://packages.microsoft.com/rhel/7/mssql-server-2019/) |
| microsoft-r-open 包 | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 路径

|||
|--|----|
| mssql/mlservices 包 | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/) |
| microsoft-r-open 包 | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>SLES/12 路径

|||
|--|----|
| mssql/mlservices 包 | [https://packages.microsoft.com/sles/12/mssql-server-2019/](https://packages.microsoft.com/sles/12/mssql-server-2019/) |
| microsoft-r-open 包 | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) | 

#### <a name="package-list"></a>包列表

根据想要使用的扩展，下载特定语言所需的包。 精确的文件名在后缀中包含平台信息，但以下文件名应足够接近，可用于确定要获取的文件。

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# R
microsoft-openmpi-3.0.0
microsoft-r-open-mkl-3.5.2
microsoft-r-open-mro-3.5.2
mssql-mlservices-packages-r-9.4.7.64
mssql-mlservices-mlm-r-9.4.7.64


# Python
microsoft-openmpi-3.0.0
mssql-mlservices-python-9.4.7.64
mssql-mlservices-packages-py-9.4.7.64
mssql-mlservices-mlm-py-9.4.7.64
```

## <a name="add-more-rpython-packages"></a>添加更多 R/Python 包 
 
可以安装其他 R 和 Python 包，并在从 SQL Server 2019 上执行的脚本中使用它们。

### <a name="r-packages"></a>R 包 
 
1. 启动 R 会话。

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R 
   ```

2. 安装名为 [glue](https://mran.microsoft.com/package/glue) 的 R 包以测试包安装。

   ```r
   # install.packages("glue",lib="/opt/mssql/mlservices/libraries/RServer") 
   ```
   也可以从命令行安装 R 包 

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R CMD INSTALL -l /opt/mssql/mlservices/libraries/RServer glue_1.1.1.tar.gz 
   ```

3. 在 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 中导入 R 包。

   ```r
   EXEC sp_execute_external_script  
   @language = N'R', 
   @script = N'library(glue)' 
   ```

### <a name="python-packages"></a>Python 包 
 
1. 使用 pip 安装名为 [httpie](https://httpie.org/) 的 Python 包。 

   ```python
   # sudo /opt/mssql/mlservices/bin/python/python -m pip install httpie 
   ``` 

2. 在 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 中导入 Python 包。
 
   ```python
   EXEC sp_execute_external_script  
   @language = N'Python',  
   @script = N'import httpie' 
   ```

## <a name="run-in-a-container"></a>在容器中运行

按照以下步骤在 Docker 容器中生成并运行 SQL Server 机器学习服务。 有关详细信息，请参阅 [在 Docker 上配置 SQL Server 容器映像](sql-server-linux-configure-docker.md)。

### <a name="prerequisites"></a>必备条件

- Git 命令行接口。
- 任何受支持的 Linux 发行版本上的 Docker 引擎 1.8 及更高版本，或用于 Mac/Windows 的 Docker。 有关详细信息，请参阅 [Install Docker](https://docs.docker.com/engine/installation/)（安装 Docker）。
- 至少 2GB 磁盘空间。
- 至少 2 GB 的 RAM。
- [Linux 上的 SQL Server 的系统要求](sql-server-linux-setup.md#system)。

### <a name="clone-the-mssql-docker-repository"></a>克隆 mssql-docker 存储库

1. 在 Linux 或 Mac 上打开 Bash 终端，或在 Windows 上打开 WSL 终端。

1. 创建本地目录，用于保留 mssql-docker 存储库的本地副本。

1. 运行 git clone 命令，以克隆 mssql-docker 存储库：

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

### <a name="build-a-sql-server-linux-container-image-with-machine-learning-services"></a>使用机器学习服务生成 SQL Server Linux 容器映像

1. 将目录更改为 mssql-mlservices 目录：

    ```bash
    cd mssql-docker/linux/preview/examples/mssql-mlservices
    ```

1. 运行 build.sh 脚本：

   ```bash
   ./build.sh
   ```

   > [!NOTE]
   > 必须安装几个 GB 大小的包，才能生成 Docker 映像。 此脚本最长可能需要 20 分钟才能完成运行，具体视网络带宽而定。

### <a name="run-the-sql-server-linux-container-image-with-machine-learning-services"></a>使用机器学习服务运行 SQL Server Linux 容器映像

1. 先设置环境变量，再运行容器。 将 PATH_TO_MSSQL 环境变量设置为主机目录：

   ```bash
    export MSSQL_PID='Developer'
    export ACCEPT_EULA='Y'
    export ACCEPT_EULA_ML='Y'
    export PATH_TO_MSSQL='/home/mssql/'
   ```

1. 运行 run.sh 脚本：

   ```bash
   ./run.sh
   ```

   此命令使用开发人员版（默认）机器学习服务创建 SQL Server 容器。 SQL Server 端口 1433 在主机上公开为端口 1401   。

   > [!NOTE]
   > 在容器中运行 SQL Server 生产版本的过程略有不同。 有关详细信息，请参阅 [在 Docker 上配置 SQL Server 容器映像](sql-server-linux-configure-docker.md)。 如果使用相同的容器名称和端口，本教程的其余部分仍适用于生产容器。

1. 若要查看 Docker 容器，请运行 `docker ps` 命令：

   ```bash
   sudo docker ps -a
   ```

1. 如果“状态”  列显示“正常运行”  状态，表明 SQL Server 正在容器中运行，且正在侦听“端口”  列中指定的端口。 如果 SQL Server 容器的“状态”列显示“已退出”，则参阅[配置指南的疑难解答部分](sql-server-linux-configure-docker.md#troubleshooting)   。

   ```bash
   $ sudo docker ps -a
   ```

    输出： 
    
    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何与 SQL Server 协同工作的基础知识。 有关下一步，请参阅以下链接：

+ [教程：在 T-SQL 中运行 R](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [教程：适用于 R 开发人员的数据库内分析](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 开发人员可以通过以下教程了解如何将 Python 与 SQL Server 一起使用：

+ [教程：在 T-SQL 中运行 Python](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [教程：适用于 Python 开发人员的数据库内分析](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

若要查看基于真实场景的机器学习示例，请参阅[机器学习教程](../advanced-analytics/tutorials/machine-learning-services-tutorials.md)。
