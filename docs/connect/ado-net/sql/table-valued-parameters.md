---
title: 表值参数
description: 介绍如何使用在 SQL Server 2008 中引入的表值参数。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 370c16d5-db7b-43e3-945b-ccaab35b739b
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: f51e5326d29d7edd6a518c02f7042cc9ed104b4f
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78895957"
---
# <a name="table-valued-parameters"></a>表值参数

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

表值参数提供了一将多行数据从客户端应用程序封送到 SQL Server 的种简单方法，而无需进行多次往返或特殊的服务器端逻辑来处理数据。 可使用表值参数来封装客户端应用程序中的数据行，并以单个参数化命令将数据发送到服务器。 传入数据行存储在随后可使用 Transact-SQL 进行操作的表变量中。  
  
可以使用标准的 Transact-SQL SELECT 语句来访问表值参数中的列值。 表值参数为强类型，其结构会自动进行验证。 表值参数的大小仅受服务器内存的限制。  
  
> [!NOTE]
>  不能在表值参数中返回数据。 表值参数仅限输入；不支持 OUTPUT 关键字。  
  
若要详细了解表值参数，请参阅以下资源。  
  
|资源|说明|  
|--------------|-----------------|  
|SQL Server 联机丛书中的[表值参数（数据库引擎）](https://go.microsoft.com/fwlink/?LinkId=98363)|介绍如何创建和使用表值参数。|  
|SQL Server 联机丛书中的[用户定义的表类型](https://go.microsoft.com/fwlink/?LinkId=98364)|说明用于声明表值参数的用户定义的表类型。|  
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>在早期版本的 SQL Server 中传递多个行  
在 SQL Server 2008 中引入表值参数之前，用于将多行数据传递到存储过程或参数化 SQL 命令的选项受到限制。 开发人员可以选择下面的一种方法，将多行传递到服务器：  
  
- 使用一系列单独的参数来表示多列和多行数据中的值。 使用这种方法可以传递的数据量受到允许使用的参数数量限制。 SQL Server 过程最多可以有 2100 个参数。 必须使用服务器端逻辑，将这些单独的值汇编到表变量或临时表中以供处理。  
  
- 将多个数据值绑定到分隔字符串或 XML 文档，然后将这些文本值传递到过程或语句。 这就需要过程或语句包括可用于验证数据结构和解绑值的必需逻辑。  
  
- 为影响多行的数据修改创建一系列单独的 SQL 语句，例如通过调用 <xref:Microsoft.Data.SqlClient.SqlDataAdapter> 的 `Update` 方法创建的语句。 可以将更改单独提交到服务器，也可以分批提交到服务器。 但是，即使分批提交包含多个语句，每个语句也会在服务器上单独执行。  
  
- 使用 `bcp` 实用工具或 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 对象将多行数据加载到表中。 尽管此方法非常有效，但它不支持服务器端处理（除非将数据加载到临时表或表变量中）。  
  
## <a name="creating-table-valued-parameter-types"></a>创建表值参数类型  
表值参数以通过使用 Transact-SQL CREATE TYPE 语句定义的强类型表结构为基础。 必须先在 SQL Server 中创建一个表类型并定义结构，才能在客户端应用程序中使用表值参数。 有关创建表类型的详细信息，请参阅 SQL Server 联机丛书中的[用户定义的表类型](https://go.microsoft.com/fwlink/?LinkID=98364)。  
  
以下语句创建一个名为 CategoryTableType 的表类型，其中包含 CategoryID 列和 CategoryName 列：  
  
```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```  
  
创建表类型后，可以基于该类型声明表值参数。 下面的 Transact-SQL 片段演示如何在存储过程定义中声明表值参数。 请注意，声明表值参数需要 READONLY 关键字。  
  
```sql
CREATE PROCEDURE usp_UpdateCategories   
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```  
  
## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>使用表值参数修改数据 (transact-SQL)  
通过执行单个语句，可以在影响多行的基于集的数据修改中使用表值参数。 例如，可以选择表值参数中的所有行并将它们插入数据库表，也可以通过将表值参数联接到要更新的表来创建更新语句。  
  
下面的 Transact-SQL UPDATE 语句演示如何通过将表值参数联接到 Categories 表来使用它。 在 FROM 子句中结合使用表值参数和 JOIN 时，还必须对表值参数使用别名。如下所示，表值参数的别名为“ec”：  
  
```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```  
  
此 Transact-SQL 示例演示如何从表值参数中选择行以在单个基于集的操作中执行 INSERT。  
  
```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```  
  
## <a name="limitations-of-table-valued-parameters"></a>表值参数的限制  
表值参数存在几个限制：  
  
- 无法将表值参数传递给 [CLR 用户定义的函数](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)。  
  
- 只能将表值参数编制索引为支持 UNIQUE 或 PRIMARY KEY 约束。 SQL Server 不维护表值参数的统计信息。  
  
- 在 Transact-SQL 代码中表值参数是只读的。 既不能更新表值参数行中的列值，也不能插入或删除行。 若要修改表值参数中传递到存储过程或参数化语句的数据，必须将数据插入临时表或表变量。  
  
- 不能使用 ALTER TABLE 语句来修改表值参数的设计。  
  
## <a name="configuring-a-sqlparameter-example"></a>配置 SqlParameter 示例  
<xref:Microsoft.Data.SqlClient> 支持从 <xref:System.Data.DataTable><xref:System.Data.Common.DbDataReader> 或 <xref:System.Collections.Generic.IEnumerable%601> \ <xref:Microsoft.Data.SqlClient.Server.SqlDataRecord> 对象填充表值参数。 必须使用 <xref:Microsoft.Data.SqlClient.SqlParameter> 的 <xref:Microsoft.Data.SqlClient.SqlParameter.TypeName%2A> 属性指定表值参数的类型名称。 `TypeName` 必须与先前在服务器上创建的兼容类型的名称相匹配。 下面的代码段演示如何配置 <xref:Microsoft.Data.SqlClient.SqlParameter> 以插入数据。  
 
在以下示例中，`addedCategories` 变量包含一个 <xref:System.Data.DataTable>。 若要查看如何填充变量，请参阅下一节中的示例，[将表值参数传递给存储过程](#passing)。

```csharp  
// Configure the command and parameter.  
SqlCommand insertCommand = new SqlCommand(sqlInsert, connection);  
SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
tvpParam.SqlDbType = SqlDbType.Structured;  
tvpParam.TypeName = "dbo.CategoryTableType";  
```   
  
你也可以使用从 <xref:System.Data.Common.DbDataReader> 中派生的任何对象，将数据行流处理到表值参数，如本代码段所示：  
  
```csharp  
// Configure the SqlCommand and table-valued parameter.  
SqlCommand insertCommand = new SqlCommand("usp_InsertCategories", connection);  
insertCommand.CommandType = CommandType.StoredProcedure;  
SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", dataReader);  
tvpParam.SqlDbType = SqlDbType.Structured;  
```  
  
## <a name="passing"></a> 将表值参数传递给存储过程  
此示例演示如何将表值参数数据传递到存储过程。 代码使用 <xref:System.Data.DataTable.GetChanges%2A> 方法将添加的行提取到新的 <xref:System.Data.DataTable> 中。 然后，该代码定义一个 <xref:Microsoft.Data.SqlClient.SqlCommand>，并将 <xref:Microsoft.Data.SqlClient.SqlCommand.CommandType%2A> 属性设置为 <xref:System.Data.CommandType.StoredProcedure>。 使用 <xref:Microsoft.Data.SqlClient.SqlParameterCollection.AddWithValue%2A> 方法填充 <xref:Microsoft.Data.SqlClient.SqlParameter>，并将 <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> 设置为 `Structured`。 然后，使用 <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> 方法执行 <xref:Microsoft.Data.SqlClient.SqlCommand>。  
  
```csharp  
// Assumes connection is an open SqlConnection object.  
using (connection)  
{  
  // Create a DataTable with the modified rows.  
  DataTable addedCategories = CategoriesDataTable.GetChanges(DataRowState.Added);  

  // Configure the SqlCommand and SqlParameter.  
  SqlCommand insertCommand = new SqlCommand("usp_InsertCategories", connection);  
  insertCommand.CommandType = CommandType.StoredProcedure;  
  SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
  tvpParam.SqlDbType = SqlDbType.Structured;  

  // Execute the command.  
  insertCommand.ExecuteNonQuery();  
}  
```  
  
### <a name="passing-a-table-valued-parameter-to-a-parameterized-sql-statement"></a>将表值参数传递给参数化 SQL 语句  
 下面的示例演示如何使用包含将表值参数作为数据源的 SELECT 子查询的 INSERT 语句向 dbo.Categories 表插入数据。 将表值参数传递给参数化 SQL 语句时，必须使用 <xref:Microsoft.Data.SqlClient.SqlParameter> 的新 <xref:Microsoft.Data.SqlClient.SqlParameter.TypeName%2A> 属性指定表值参数的类型名称。 此 `TypeName` 必须与先前在服务器上创建的兼容类型的名称相匹配。 本示例中的代码使用 `TypeName` 属性来引用在 dbo.CategoryTableType 中定义的类型结构。  
  
> [!NOTE]
>  如果为表值参数中的标识列提供值，则必须为会话发出 SET IDENTITY_INSERT 语句。  
  
```csharp  
// Assumes connection is an open SqlConnection.  
using (connection)  
{  
  // Create a DataTable with the modified rows.  
  DataTable addedCategories = CategoriesDataTable.GetChanges(DataRowState.Added);  

  // Define the INSERT-SELECT statement.  
  string sqlInsert =   
      "INSERT INTO dbo.Categories (CategoryID, CategoryName)"  
      + " SELECT nc.CategoryID, nc.CategoryName"  
      + " FROM @tvpNewCategories AS nc;"  

  // Configure the command and parameter.  
  SqlCommand insertCommand = new SqlCommand(sqlInsert, connection);  
  SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
  tvpParam.SqlDbType = SqlDbType.Structured;  
  tvpParam.TypeName = "dbo.CategoryTableType";  

  // Execute the command.  
  insertCommand.ExecuteNonQuery();  
}  
```  
  
## <a name="streaming-rows-with-a-datareader"></a>使用 DataReader 流式处理行  
你也可以使用从 <xref:System.Data.Common.DbDataReader> 中派生的任何对象，将数据行流处理到表值参数。 下面的代码段演示如何使用 <xref:System.Data.OracleClient.OracleCommand> 和 <xref:System.Data.OracleClient.OracleDataReader> 从 Oracle 数据库中检索数据。 然后，该代码将 <xref:Microsoft.Data.SqlClient.SqlCommand> 配置为使用单个输入参数调用存储过程。 <xref:Microsoft.Data.SqlClient.SqlParameter> 的 <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> 属性设置为 `Structured`。 <xref:Microsoft.Data.SqlClient.SqlParameterCollection.AddWithValue%2A> 将 `OracleDataReader` 结果集作为表值参数传递给存储过程。  
  
```csharp  
// Assumes connection is an open SqlConnection.  
// Retrieve data from Oracle.  
OracleCommand selectCommand = new OracleCommand(  
   "Select CategoryID, CategoryName FROM Categories;",  
   oracleConnection);  
OracleDataReader oracleReader = selectCommand.ExecuteReader(  
   CommandBehavior.CloseConnection);  
  
 // Configure the SqlCommand and table-valued parameter.  
 SqlCommand insertCommand = new SqlCommand(  
   "usp_InsertCategories", connection);  
 insertCommand.CommandType = CommandType.StoredProcedure;  
 SqlParameter tvpParam =  
    insertCommand.Parameters.AddWithValue(  
    "@tvpNewCategories", oracleReader);  
 tvpParam.SqlDbType = SqlDbType.Structured;  
  
 // Execute the command.  
 insertCommand.ExecuteNonQuery();  
```  
  
## <a name="next-steps"></a>后续步骤
- [ADO.NET 中的 SQL Server 数据操作](sql-server-data-operations.md)
