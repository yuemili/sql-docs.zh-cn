---
title: IHarticles （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHarticles
- IHarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHarticles system table
ms.assetid: 773ef9b7-c993-4629-9516-70c47b9dcf65
author: stevestein
ms.author: sstein
ms.openlocfilehash: 45278a6d9501b75b624e11bbeb11d24d10e482c6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68056209"
---
# <a name="iharticles-transact-sql"></a>IHarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用当前分发服务器从非 SQL Server 发布服务器复制的每个项目在**IHarticles**系统表中各占一行。 此表存储在分发数据库中。  
  
## <a name="definition"></a>定义  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|为项目提供唯一 ID 号的标识列。|  
|**路径名**|**sysname**|与项目关联的名称，在发布内是唯一的。|  
|**publication_id**|**smallint**|项目所属发布的 ID。|  
|table_id |**int**|要从[IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md)发布的表的 ID。|  
|**publisher_id**|**smallint**|非 SQL Server 发布服务器的 ID。|  
|**creation_script**|**nvarchar(255)**|项目的架构脚本。|  
|**del_cmd**|**nvarchar(255)**|复制对表项目的删除操作时所使用的复制命令类型。 有关详细信息，请参阅[指定如何传播事务项目的更改](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。|  
|**筛选器**|**int**|此列未使用，只是为了使**IHarticles**表的[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图与用于 SQL Server 文章（[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)）的[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图兼容。|  
|**filter_clause**|**ntext**|项目的 WHERE 子句，用于水平筛选并以非 SQL 发布服务器可以解释的标准 Transact-SQL 编写。|  
|**ins_cmd**|**nvarchar(255)**|复制对表项目的插入操作时所使用的复制命令类型。 有关详细信息，请参阅[指定如何传播事务项目的更改](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。|  
|**pre_creation_cmd**|**tinyint**|当订阅服务器中已经存在同名对象时，将应用在初始快照之前执行的命令。<br /><br /> **0** = 无-不执行命令。<br /><br /> **1** = 放置目标表。<br /><br /> **2** = 删除-删除目标表中的数据。<br /><br /> **3** = 截断-截断目标表。|  
|**状态值**|**tinyint**|项目选项和状态的位掩码，可以是对以下一个或多个值执行逻辑位或运算的结果：<br /><br /> **0** = 无附加属性。<br /><br /> **1** = 活动。<br /><br /> **8** = 在 INSERT 语句中包括列名称。<br /><br /> **16** = 使用参数化语句。<br /><br /> 例如，使用参数化语句的活动项目在此列中的值为 17。 如果值为 0，则表示项目处于非活动状态，而且未定义其他属性。|  
|type |**tinyint**|项目的类型：<br /><br /> **1** = 基于日志的项目。|  
|**upd_cmd**|**nvarchar(255)**|复制对表项目的更新操作时所使用的复制命令类型。 有关详细信息，请参阅[指定如何传播事务项目的更改](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。|  
|**schema_option**|**binary （8）**|给定项目的架构生成选项的位图，它可以是下面的一个或多个值的位逻辑或结果：<br /><br /> **0x00** = 快照代理禁用脚本，并使用提供的 CreationScript。<br /><br /> **0x01** = 生成对象创建（CREATE TABLE、创建过程等）。<br /><br /> **0x10** = 生成相应的聚集索引。<br /><br /> **0x40** = 生成相应的非聚集索引。<br /><br /> **0x80** = 在主键上包含已声明的引用完整性。<br /><br /> **0x1000** = 复制列级排序规则。 注意：默认情况下，将为 Oracle 发布服务器设置此选项，以启用区分大小写的比较。<br /><br /> **0x4000** = 复制表项目中定义的唯一键。<br /><br /> **0x8000** = 使用 ALTER table 语句将表项目上的主键和唯一键作为约束复制。|  
|**dest_owner**|**sysname**|目标数据库中表的所有者。|  
|**dest_table**|**sysname**|目标表的名称。|  
|**tablespace_name**|**nvarchar(255)**|标识项目的日志记录表使用的表空间。|  
|**objid**|**int**|此列未使用，只是为了使**IHarticles**表的[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图与用于 SQL Server 文章（[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)）的[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图兼容。|  
|**sync_objid**|**int**|此列未使用，只是为了使**IHarticles**表的[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图与用于 SQL Server 文章（[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)）的[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图兼容。|  
|**2008**|**nvarchar(255)**|项目的描述性条目。|  
|**publisher_status**|**int**|用于指示是否已通过调用[sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)定义了用于定义已发布项目的视图。<br /><br /> **已调用 0** = [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 。<br /><br /> **** = 尚未调用1个[sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 。|  
|**article_view_owner**|**nvarchar(255)**|发布服务器上由日志读取器代理使用的同步对象的所有者。|  
|**article_view**|**nvarchar(255)**|发布服务器上由日志读取器代理使用的同步对象。|  
|**ins_scripting_proc**|**int**|此列未使用，只是为了使**IHarticles**表的[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图与用于 SQL Server 文章（[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)）的[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图兼容。|  
|**del_scripting_proc**|**int**|此列未使用，只是为了使**IHarticles**表的[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图与用于 SQL Server 文章（[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)）的[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图兼容。|  
|**upd_scripting_proc**|**int**|此列未使用，只是为了使**IHarticles**表的[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图与用于 SQL Server 文章（[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)）的[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图兼容。|  
|**custom_script**|**int**|此列未使用，只是为了使**IHarticles**表的[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图与用于 SQL Server 文章（[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)）的[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图兼容。|  
|**fire_triggers_on_snapshot**|**bit**|此列未使用，只是为了使**IHarticles**表的[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图与用于 SQL Server 文章（[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)）的[sysarticles](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)视图兼容。|  
|**instance_id**|**int**|标识已发布表的项目日志的当前实例。|  
|**use_default_datatypes**|**bit**|指示项目是否使用默认数据类型映射;如果值为**1** ，则表示使用默认的数据类型映射。|  
  
## <a name="see-also"></a>另请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Transact-sql&#41;&#40;复制视图](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)  
  
  
