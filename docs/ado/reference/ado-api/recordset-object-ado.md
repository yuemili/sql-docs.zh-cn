---
title: Recordset 对象（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: ede1415f-c3df-4cc5-a05b-2576b2b84b60
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e76bc993b6f3fed781b8458bc7cf4a70081cd167
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931367"
---
# <a name="recordset-object-ado"></a>记录集对象 (ADO)
表示基表中的整个记录集或执行的命令的结果。 **记录集**对象随时仅指集内的单个记录作为当前记录。  
  
## <a name="remarks"></a>备注  
 您可以使用**Recordset**对象处理来自提供程序的数据。 使用 ADO 时，几乎完全可以使用**Recordset**对象处理数据。 所有**记录集**对象均由记录（行）和字段（列）组成。 某些**记录集**方法或属性可能不可用，具体取决于提供程序支持的功能。  
  
 ADODB.RECORDSET.记录集是应用于创建**记录集**对象的 ProgID。 引用过时 ADOR 的现有应用程序。记录集 ProgID 将继续运行而无需重新编译，但新开发应引用 ADODB.RECORDSET。记录集.  
  
 在 ADO 中定义了四种不同的游标类型：  
  
-   **动态游标**允许您查看其他用户的添加、更改和删除操作;允许所有类型的移动都通过不依赖于书签的**记录集**;如果提供程序支持，则和允许书签。  
  
-   **键集游标**的行为类似于动态游标，只不过它会阻止你查看其他用户添加的记录，并阻止访问其他用户删除的记录。 其他用户所做的数据更改仍将可见。 它始终支持书签，因此允许所有类型的移动都通过**记录集**。  
  
-   **静态游标**提供一组记录的静态副本，您可以使用它们来查找数据或生成报表;始终允许使用书签，因此允许在**记录集中**进行所有类型的移动。 其他用户的添加、更改或删除将不可见。 这是在打开客户端**记录集**对象时允许的唯一游标类型。  
  
-   **只进游标**仅允许在**记录集中**向前滚动。 其他用户的添加、更改或删除将不可见。 这可以提高在需要仅通过**记录集**进行一次传递的情况下的性能。  
  
 请在打开**记录集**之前设置[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)属性以选择游标类型，或使用[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法传递*CursorType*参数。 某些提供程序不支持所有游标类型。 查看提供程序的文档。 如果未指定游标类型，则默认情况下 ADO 会打开只进游标。  
  
 如果[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**AdUseClient**以打开**记录集**，则[字段](../../../ado/reference/ado-api/field-object.md)对象上的**UnderlyingValue**属性在返回的**recordset**对象中不可用。 与某些提供程序一起使用时（例如用于 OLE DB 的 Microsoft ODBC 提供程序与 Microsoft SQL Server 结合使用），可以通过使用**Open**方法传递连接字符串，独立于先前定义的[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象创建**记录集**对象。 ADO 仍创建一个[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象，但它不会将该对象分配给对象变量。 但是，如果在同一连接上打开多个**记录集**对象，则应显式创建并打开一个**连接**对象;这会将**连接**对象分配给对象变量。 如果在打开**记录集**对象时不使用此对象变量，则 ADO 将为每个新**记录集**创建新的**连接**对象，即使传递相同的连接字符串也是如此。  
  
 您可以根据需要创建任意数量的**记录集**对象。  
  
 打开**记录集**时，当前记录将定位到第一条记录（如果有）， [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)和[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)属性将设置为**False**。 如果没有任何记录，则**BOF**和**EOF**属性设置为**True**。  
  
 可使用[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 **MoveLast**、 **MoveNext**和**MovePrevious**方法;[Move](../../../ado/reference/ado-api/move-method-ado.md)方法;以及[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)、 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)和[Filter](../../../ado/reference/ado-api/filter-property.md)属性，用于重定位当前记录（假定提供程序支持相关功能）。 只进**记录集**对象仅支持[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法。 当您使用**移动**方法来访问每个记录（或枚举**记录集**）时，您可以使用**BOF**和**EOF**属性来确定是否已移出**记录集**的开头或结尾。  
  
 使用**Recordset**对象的任何功能之前，必须对对象调用**支持**方法，以验证该功能是否受支持或可用。 如果**支持**方法返回 false，则不得使用该功能。 例如，如果`Recordset.Supports(adMovePrevious)`返回**True**，则可以使用**MovePrevious**方法。 否则，你将收到一个错误，因为**记录集**对象可能已关闭，并且该实例上呈现的功能不可用。 如果你感兴趣的功能不受支持，则**支持**将返回 false。 在这种情况下，应避免在**Recordset**对象上调用相应的属性或方法。  
  
 **记录集**对象可以支持两种类型的更新：即时和批处理。 在立即更新中，一旦调用[Update](../../../ado/reference/ado-api/update-method.md)方法，对数据所做的所有更改都会立即写入基础数据源。 你还可以使用[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)和**Update**方法将值数组作为参数传递，并同时更新记录中的多个字段。  
  
 如果提供程序支持批处理更新，则可以将提供程序缓存更改为多个记录，然后使用[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法通过对数据库的单个调用传输这些记录。 这适用于通过**AddNew**、 **Update**和[Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)方法所做的更改。 调用**UpdateBatch**方法后，可以使用[状态](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性来检查是否存在任何数据冲突，以便解决这些问题。  
  
> [!NOTE]
>  若要在不使用[命令](../../../ado/reference/ado-api/command-object-ado.md)对象的情况下执行查询，请将查询字符串传递到**Recordset**对象的**Open**方法。 但是，当你想要保留命令文本并重新执行它，或使用查询参数时，需要使用**命令**对象。  
  
 [Mode](../../../ado/reference/ado-api/mode-property-ado.md)属性控制访问权限。  
  
 **Fields**集合是**Recordset**对象的默认成员。 因此，下面两个代码语句是等效的。  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 当跨进程传递**Recordset**对象时，只会封送**行集**值并忽略**记录集**对象的属性。 在 unmarshalling 期间，**行集**将解压缩到新创建的**记录集**对象，该对象还会将其属性设置为默认值。  
  
 对于脚本编写， **Recordset**对象是安全的。  
  
 本部分包含以下主题。  
  
-   [记录集对象属性、方法和事件](../../../ado/reference/ado-api/recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [Connection 对象（ADO）](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Fields 集合（ADO）](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties 集合（ADO）](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [附录 A：提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)
