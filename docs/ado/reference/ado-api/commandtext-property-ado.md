---
title: CommandText 属性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandText
helpviewer_keywords:
- CommandText property [ADO]
ms.assetid: 4dd7e82a-8da5-4a4e-b439-11a29286fa0e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0288dde74d2a172c9b0f8bdb865f4467fb0f637
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919729"
---
# <a name="commandtext-property-ado"></a>CommandText 属性 (ADO)
指示要对提供程序发出的命令的文本。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 获取或设置一个**字符串**值，该值包含提供程序命令，如 SQL 语句、表名、相对 URL 或存储过程调用。 默认值为空字符串（""）。  
  
## <a name="remarks"></a>备注  
 使用**CommandText**属性可以设置或返回[命令](../../../ado/reference/ado-api/command-object-ado.md)对象表示的命令的文本。 通常，这将是一条 SQL 语句，但也可以是提供程序所识别的任何其他类型的命令语句，如存储过程调用。 SQL 语句必须是提供程序的查询处理器支持的特定方言或版本。  
  
 如果在设置**CommandText**属性时，**命令**对象的已[准备](../../../ado/reference/ado-api/prepared-property-ado.md)属性设置为**True** ，并且**命令**对象绑定到打开的连接，则在调用[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)或[open](../../../ado/reference/ado-api/open-method-ado-connection.md)方法时，ADO 将准备该查询（即，提供程序存储的已编译的查询形式）。  
  
 根据[CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)属性设置，ADO 可能会改变**CommandText**属性。 您可以随时读取**CommandText**属性，以查看 ADO 在执行过程中将使用的实际命令文本。  
  
 使用**CommandText**属性可以设置或返回一个相对 URL，该 URL 指定一个资源，如文件或目录。 资源相对于由绝对 URL 显式指定的位置，或由打开的[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象隐式。  
  
> [!NOTE]
>  使用 http 方案的 Url 将自动调用[用于 Internet 发布的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>应用于  
 [命令对象 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 属性示例（VB）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 属性示例（VC + +）](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Requery 方法](../../../ado/reference/ado-api/requery-method.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size 和 Direction 属性示例（JScript）](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
