---
title: 运行通讯簿示例应用程序 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 3a2644e9-d634-4ae6-a5b7-13fb7b317ec7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 45324642d2f323297ecbe091617fbb14cc5fc785
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922240"
---
# <a name="running-the-address-book-sample-application"></a>运行通讯簿示例应用程序
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 若要运行通讯簿应用程序，请按照此过程操作。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
### <a name="to-run-this-application"></a>运行此应用程序  
  
1.  请确保 Microsoft SQL Server 正在运行。 单击 "**开始**"，依次指向 "**程序**"、 **Microsoft SQL Server 7.0**"，然后单击" **Service Manager**"。 如果白圆圈中有一个绿色箭头，则 SQL Server 正在运行。 如果没有，请单击 "**开始"/"继续**"。  
  
2.  在 Microsoft Internet Explorer 4.0 或更高版本中，键入以下地址：  
  
     **https://** *web*服务器 **/RDS/AddressBook/AddrBook.asp**  
  
     其中 *，web 服务器*是安装 RDS server 组件的 Web 服务器的名称。  
  
3.  然后，你可以在通讯簿示例应用程序中尝试各种方案，例如，基于其电子邮件名称搜索某个用户，列出所有标题为 "项目经理" 的人员或编辑现有记录。 单击 "**查找**" 以使用所有可用名称填充数据网格。  
  
## <a name="see-also"></a>另请参阅  
 [通讯簿数据绑定对象](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)




