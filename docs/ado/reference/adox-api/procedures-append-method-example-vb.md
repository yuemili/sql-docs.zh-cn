---
title: 过程 Append 方法示例（VB） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Append method [ADOX], Visual Basic example
ms.assetid: ce83b966-474b-4f57-8eb9-370996dfc5c0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8bacc5dc2d55fb335358ab9ca34248f8e322811a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965427"
---
# <a name="procedures-append-method-example-vb"></a>过程 Append 方法示例 (VB)
下面的代码演示了如何使用[命令](../../../ado/reference/ado-api/command-object-ado.md)对象和[过程](../../../ado/reference/adox-api/procedures-collection-adox.md)集合[Append](../../../ado/reference/adox-api/append-method-adox-procedures.md)方法在基础数据源中创建新的过程。  
  
```  
' BeginCreateProcedureVB  
Sub Main()  
    On Error GoTo CreateProcedureError  
  
    Dim cnn As New ADODB.Connection  
    Dim cmd As New ADODB.Command  
    Dim prm As ADODB.Parameter  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Connection  
    cnn.Open _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Create the parameterized command (Microsoft Jet specific)  
    Set cmd.ActiveConnection = cnn  
    cmd.CommandText = "PARAMETERS [CustId] Text;" & _  
    "Select * From Customers Where CustomerId = [CustId]"  
  
    ' Open the Catalog  
    Set cat.ActiveConnection = cnn  
  
    ' Create the new Procedure  
    cat.Procedures.Append "CustomerById", cmd  
  
    'Clean  
    cnn.Close  
    Set cat = Nothing  
    Set cmd = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
CreateProcedureError:  
    Set cat = Nothing  
    Set cmd = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCreateProcedureVB  
```  
  
## <a name="see-also"></a>另请参阅  
 [ActiveConnection 属性（ADOX）](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [Append 方法（ADOX 过程）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [目录对象（ADOX）](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Procedure 对象（ADOX）](../../../ado/reference/adox-api/procedure-object-adox.md)   
 [过程集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)
