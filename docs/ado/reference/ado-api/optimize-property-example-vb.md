---
title: Optimize 属性示例（VB） |Microsoft Docs
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
- Optimize property [ADO], Visual Basic example
ms.assetid: 652194af-cfa4-4aa0-a6d6-fa409bbc3f98
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f36c0c574917e4f73533a400ea60f363aeb9d74b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917815"
---
# <a name="optimize-property-example-vb"></a>Optimize 属性示例 (VB)
此示例演示[字段](../../../ado/reference/ado-api/field-object.md)对象的 "动态**优化**" 属性。 不会为***Pubs***数据库中***作者***表的***zip***字段编制索引。 将 "***压缩***" 字段中的 "[优化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)" 属性设置为 " **True** " 可授予 ADO 生成索引，从而提高[Find](../../../ado/reference/ado-api/find-method-ado.md)方法的性能。  
  
```  
'BeginOptimizeVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string.  
  
    ' Declare the recordset and connection variables.  
    Dim Cnxn As ADODB.Connection  
    Dim rstAuthors As ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQLAuthors As String  
  
     ' Open connection.  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Set Cnxn = New ADODB.Connection  
    Cnxn.Open strCnxn  
  
     ' open recordset client-side to enable index creation.  
    Set rstAuthors = New ADODB.Recordset  
    rstAuthors.CursorLocation = adUseClient  
    strSQLAuthors = "SELECT * FROM Authors"  
    rstAuthors.Open strSQLAuthors, Cnxn, adOpenStatic, adLockReadOnly, adCmdText  
     ' Create the index.  
    rstAuthors!zip.Properties("Optimize") = True  
     ' Find Akiko Yokomoto  
    rstAuthors.Find "zip = '94595'"  
  
     ' Show results.  
    Debug.Print rstAuthors!au_fname & " " & rstAuthors!au_lname & " " & _  
             rstAuthors!address & " " & rstAuthors!city & " " & rstAuthors!State  
    rstAuthors!zip.Properties("Optimize") = False  'Delete the index.  
  
    ' Clean up.  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndOptimizeVB  
```  
  
## <a name="see-also"></a>另请参阅  
 [Field 对象](../../../ado/reference/ado-api/field-object.md)   
 [Optimize 属性 - 动态 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
