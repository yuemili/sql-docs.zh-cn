---
title: 表属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql12.swb.tableproperties.storage.f1
- sql12.SWB.SELECTCOLUMNS.F1
- sql12.swb.tableproperties.filetable.f1
- sql12.swb.tableproperties.general.f1
- sql12.swb.tableproperties.changetracking.f1
ms.assetid: ad8a2fd4-f092-4c0f-be85-54ce8b9d725a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b07f157294700b3b3b7958ce4cdc6f1589bff864
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68196710"
---
# <a name="table-properties"></a>表的属性
  本主题介绍在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的“表属性”对话框中显示的表属性。 有关如何显示这些属性的详细信息，请参阅 [查看表定义](view-the-table-definition.md)。  
  
 **本主题内容**  
  
1.  [“常规”页](#GeneralPage)  
  
2.  [“更改跟踪”页](#ChangeTracking)  
  
3.  [“文件表”页](#FileTable)  
  
4.  [“存储”页](#Storage)  
  
##  <a name="GeneralPage"></a> “常规”页  
 **Database**  
 包含此表的数据库的名称。  
  
 **Server**  
 当前服务器实例的名称。  
  
 **用户**  
 此连接的用户名。  
  
 **创建日期**  
 该表的创建日期和时间。  
  
 **名称**  
 表的名称。  
  
 **架构**  
 该表所属的架构。  
  
 **系统对象**  
 指示此表为系统表， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用此表来保存内部信息。 用户不要直接更改或引用系统表。  
  
 **ANSI NULLs**  
 指示在创建对象时 ANSI NULL 选项是否设为 ON。 有关详细信息，请参阅 [SET ANSI_NULLS (Transact SQL)](/sql/t-sql/statements/set-ansi-nulls-transact-sql)  
  
 **带引号的标识符**  
 指示在创建对象时带引号的标识符选项是否设为 ON。 有关详细信息，请参阅 [SET QUOTED_IDENTIFIER (Transact SQL)](/sql/t-sql/statements/set-quoted-identifier-transact-sql)  
  
 **锁升级**  
 指示表的锁升级粒度。 有关数据库引擎中的锁定的详细信息，请参阅 [SQL Server 事务锁定和行版本控制指南](https://msdn.microsoft.com/library/jj856598.aspx)。 可能的值包括：  
  
 AUTO  
 此选项可让 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 选择适合于表架构的锁升级粒度。  
  
-   如果该表已分区，则允许锁升级到堆或 B 树 (HoBT) 粒度。 锁升级到 HoBT 级别之后，该锁以后将不会升级到 TABLE 粒度。  
  
-   如果该表未分区，则会将锁升级到 TABLE 粒度。  
  
 TABLE  
 无论表是否已分区，都会将锁升级到表级粒度。 默认值为 TABLE。  
  
 DISABLE  
 在大多数情况下禁止锁升级。 表级别的锁未完全禁止。 例如，当扫描在可序列化隔离级别下没有聚集索引的表时， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 必须使用表锁来保证数据的完整性。  
  
 **表已复制**  
 指示是否使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制将表复制到其他数据库。 可能的值为 `True` 或 `False`。  
  
##  <a name="ChangeTracking"></a>更改跟踪页面  
 **更改跟踪**  
 指示是否对相应的表启用了更改跟踪。 默认值是 `False`。  
  
 只有对数据库启用了更改跟踪，此选项才可用。  
  
 若要启用更改跟踪，相应的表必须具有一个主键，且您必须拥有修改该表的权限。 您可以使用 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql)来配置更改跟踪。  
  
 **跟踪已更新的列**  
 指示 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 是否跟踪哪些列已更新。  
  
 有关更改跟踪的详细信息，请参阅[关于更改跟踪 (SQL Server)](../track-changes/about-change-tracking-sql-server.md)。  
  
##  <a name="FileTable"></a>FileTable 页  
 显示与 FileTable 相关的表的属性。 有关详细信息，请参阅 [FileTables (SQL Server)](../blob/filetables-sql-server.md)。  
  
 **FileTable 名称列排序规则**  
 应用于 FileTable 的 **Name** 列的排序规则。 该 **Name** 列包含文件和目录名称。  
  
 **FileTable 目录名称**  
 FileTable 的根文件夹。  
  
 **已启用 FileTable 命名空间**  
 在为 `True` 时，该值指示该表为 FileTable。 如果您将该值更改为 `False`，则是在将 FileTable 更改为普通用户表。 如果您以后想要将该表更改回 FileTable，则该表将必须首先通过 FileTable 一致性检查，之后转换才会成功。  
  
##  <a name="Storage"></a>存储页  
 显示所选表中与存储相关的属性。  
  
### <a name="compression"></a>压缩  
 **压缩类型**  
 表的压缩类型。 此属性仅可用于未分区的表。 有关详细信息，请参阅 [Data Compression](../data-compression/data-compression.md)。  
  
 **使用页压缩的分区**  
 使用页压缩的分区号。 此属性仅可用于已分区表。  
  
 **未压缩的分区**  
 未压缩的分区号。 此属性仅可用于已分区表。  
  
 **使用行压缩的分区**  
 使用行压缩的分区号。 此属性仅可用于已分区表。  
  
### <a name="filegroup"></a>文件组  
 **文本文件组**  
 包含该表文本数据的文件组的名称。  
  
 **文件**  
 包含该表的文件组的名称。  
  
 **表已分区**  
 可能的值为 `True` 和 `False`。  
  
 **Filestream 文件组**  
 如果该表包含具有 FILESTREAM 属性的 `varbinary(max)` 列，则指定 FILESTREAM 数据文件组的名称。 默认值为默认的 FILESTREAM 数据文件组。  
  
 如果该表不包含 FILESTREAM 数据，则该字段为空白。  
  
### <a name="general"></a>常规  
 **Vardecimal 存储格式已启用**  
 如果`True`为，则此只读值表示使用`decimal` vardecimal `numeric`存储格式存储和数据类型。 若要更改此选项，请`vardecimal storage format`使用[sp_tableoption](/sql/relational-databases/system-stored-procedures/sp-tableoption-transact-sql)的选项。 不推荐使用 Vardecimal 存储格式。 请改用 ROW 压缩。  
  
 **索引空间**  
 索引在表中所占的空间大小 (MB)。 此值不包括表的 XML 索引空间使用量。 如果 XML 索引属于表，则使用 [sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql) 。  
  
 **行计数**  
 该表中的行数。  
  
 **数据空间**  
 数据在表中所占的空间大小 (MB)。  
  
### <a name="partitioning"></a>分区  
 此部分仅适用于已进行分区的表。 有关详细信息，请参阅 [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md)。  
  
 **分区列**  
 对表进行分区时所依据的列的名称。  
  
 **分区方案**  
 如果表已分区，则为分区方案的名称。 如果表未分区，则该字段为空白。  
  
 **分区数**  
 表中的分区数。  
  
 **FILESTREAM 分区方案**  
 如果表已分区，则为 FILESTREAM 分区方案的名称。 如果表未分区，则该字段为空白。  
  
 FILESTREAM 分区方案必须与 **“分区方案”** 选项中指定的方案对称。  
  
## <a name="see-also"></a>另请参阅  
 [查看表定义](view-the-table-definition.md)   
 [数据库引擎&#41;修改列 &#40;](../tables/modify-columns-database-engine.md)  
  
  
