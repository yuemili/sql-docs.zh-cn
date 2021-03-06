---
title: 监视可用性组 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- dynamic management views [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], listeners
- Availability Groups [SQL Server], databases
- catalog views [SQL Server], AlwaysOn Availability Groups
ms.assetid: 881a34de-8461-4811-8c62-322bf7226bed
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4b97d62e7dede1cbbe4229f824407946f2fe43ba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62789816"
---
# <a name="monitor-availability-groups-transact-sql"></a>监视可用性组 (Transact-SQL)
  为了使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)]来监视可用性组和副本及关联的数据库， [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 提供了一组目录视图和动态管理视图及服务器属性。 通过使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] SELECT 语句，您可以使用这些视图监视可用性组及其副本和数据库。 为给定可用性组返回的信息取决于您连接到的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例承载的是主副本还是辅助副本。  
  
> [!TIP]  
>  可以使用这些视图的 ID 列来联接很多视图，以便在单个查询中返回多个视图的信息。  
  
 
  
##  <a name="Permissions"></a> 权限  
 
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 目录视图要求具有服务器实例的 VIEW ANY DEFINITION 权限。 
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 动态管理视图要求具有服务器的 VIEW SERVER STATE 权限。  
  
##  <a name="AoAgFeatureOnSI"></a>监视服务器实例上的 AlwaysOn 可用性组功能  
 若要监视服务器实例上的 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 功能，请使用以下内置函数：  
  
 [SERVERPROPERTY](/sql/t-sql/functions/serverproperty-transact-sql)函数  
 返回有关是否已启用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 的服务器属性信息；如果已启用，则返回其在服务器实例上是否启动的信息。  
  
 **列名：** IsHadrEnabled、HadrManagerStatus  
  
##  <a name="WSFC"></a>监视 WSFC 群集上的可用性组  
 若要监视 Windows Server 故障转移群集 (WSFC) 群集（承载启用了 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]的本地服务器实例），请使用以下视图：  
  
 [sys.dm_hadr_cluster](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql)  
 如果承载启用了 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 的 SQL Server 实例的 Windows Server 故障转移群集 (WSFC) 节点具有 WSFC 仲裁，则 **sys.dm_hadr_cluster** 将返回公开群集名称和仲裁信息的一行。 如果 WSFC 节点没有仲裁，则不会返回任何行。  
  
 **列名：** cluster_name、quorum_type、quorum_type_desc、quorum_state、quorum_state_desc  
  
 [sys.dm_hadr_cluster_members](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql)  
 如果承载启用了 AlwaysOn 的 SQL Server 本地实例的 WSFC 节点具有 WSFC 仲裁，则为构成仲裁的每一个成员及各个成员的状态都返回一行。  
  
 **列名：** member_name、member_type、member_type_desc、member_state、member_state_desc、number_of_quorum_votes  
  
 [sys.dm_hadr_cluster_networks](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql)  
 为每个参与可用性组子网配置的成员都返回一行。 您可以使用此动态管理视图来验证为每个可用性副本配置的网络虚拟 IP。  
  
 **列名：** member_name、network_subnet_ip、network_subnet_ipv4_mask、network_subnet_prefix_length、is_public、is_ipv4  
  
 **主键：** member_name + network_subnet_IP + network_subnet_prefix_length  
  
 [sys.dm_hadr_instance_node_map](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-instance-node-map-transact-sql)  
 对于承载加入其 AlwaysOn 可用性组的可用性副本的每个 SQL Server 实例，将返回承载该服务器实例的 Windows Server 故障转移群集 (WSFC) 节点的名称。 此动态管理视图具有以下用法：  
  
-   此动态管理视图对于检测包含承载于同一 WSFC 节点上的多个可用性副本的可用性组很有用，这是一个不受支持的配置，如果可用性组的配置不正确，则在进行 FCI 故障转移后可能出现此配置。  
  
-   当多个 SQL Server 实例承载于同一 WSFC 节点上时，资源 DLL 将使用此动态管理视图来确定要连接到的 SQL Server 实例。  
  
 **列名：** ag_resource_id、instance_name node_name  
  
 [sys.dm_hadr_name_id_map](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-name-id-map-transact-sql)  
 显示 AlwaysOn 可用性组的映射，即当前的 SQL Server 实例已联接到三个唯一 ID：一个可用性组 ID、一个 WSFC 资源 ID 和一个 WSFC 组 ID。 此映射旨在处理重命名 WSFC 资源/组的情形。  
  
 **列名：** ag_name、ag_id、ag_resource_id、ag_group_id  
  
> [!NOTE]  
>  另请参阅本主题后面**监视可用性副本**部分的 **sys.dm_hadr_availability_replica_cluster_nodes** 和 [sys.dm_hadr_availability_replica_cluster_states](#AvReplicas) 以及**监视可用性数据库**部分的 **sys.availability_databases_cluster** 和 [sys.dm_hadr_database_replica_cluster_states](#AvDbs)。  
  
 有关 WSFC 群集和[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]的信息，请参阅[Windows Server 故障转移群集 &#40;WSFC&#41; 与 SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)和[故障转移群集并 AlwaysOn 可用性组 &#40;](failover-clustering-and-always-on-availability-groups-sql-server.md)SQL Server&#41;。  
  
##  <a name="AvGroups"></a>监视可用性组  
 若要监视服务器实例为其承载可用性副本的可用性组，请使用以下视图：  
  
 [sys.availability_groups](/sql/relational-databases/system-catalog-views/sys-availability-groups-transact-sql)  
 为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的本地实例承载其可用性副本的每个可用性组返回一行。 每一行都包含可用性组元数据的缓存的副本。  
  
 **列名：** group_id、name、resource_id、resource_group_id、failure_condition_level、health_check_timeout、automated_backup_preference、automated_backup_preference_desc  
  
 [sys.availability_groups_cluster](/sql/relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql)  
 为 WSFC 群集中的每个可用性组返回一行。 每一行均包含 Windows Server 故障转移群集 (WSFC) 群集中的可用性组元数据。  
  
 **列名：** group_id、name、resource_id、resource_group_id、failure_condition_level、health_check_timeout、automated_backup_preference、automated_backup_preference_desc  
  
 [sys.dm_hadr_availability_group_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql)  
 为在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的本地实例上拥有可用性副本的每个可用性组返回一行。 每行显示定义给定可用性组的运行状况的状态。  
  
 **列名：** group_id、primary_replica、primary_recovery_health、primary_recovery_health_desc、secondary_recovery_health、secondary_recovery_health_desc、synchronization_health、synchronization_health_desc  
  
##  <a name="AvReplicas"></a>监视可用性副本  
 若要监视可用性副本，请使用以下视图和系统函数：  
  
 [sys.availability_replicas](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)  
 为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的本地实例承载其可用性副本的每个可用性组中的每个可用性副本返回一行。  
  
 **列名：** replica_id、group_id、replica_metadata_id、replica_server_name、owner_sid、endpoint_url、availability_mode、availability_mode_desc、failover_mode、failover_mode_desc、session_timeout、primary_role_allow_connections、primary_role_allow_connections_desc、secondary_role_allow_connections、secondary_role_allow_connections_desc、create_date、modify_date、backup_priority、read_only_routing_url  
  
 [sys.availability_read_only_routing_lists](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)  
 为 WSFC 故障转移群集中 AlwaysOn 可用性组的每个可用性副本的只读路由列表返回一行。  
  
 **列名：** replica_id、routing_priority、read_only_replica_id  
  
 [sys.dm_hadr_availability_replica_cluster_nodes](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-nodes-transact-sql)  
 为 Windows Server 故障转移群集 (WSFC) 群集中 AlwaysOn 可用性组的每个可用性副本（不论联接状态如何）都返回一行。  
  
 **列名：** group_name、replica_server_name、node_name  
  
 [sys.dm_hadr_availability_replica_cluster_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql)  
 为 Windows Server 故障转移群集 (WSFC) 群集中所有 AlwaysOn 可用性组（不论副本位于何处）的每个副本（不论联接状态如何）都返回一行。  
  
 **列名：** replica_id、replica_server_name、group_id、join_state、join_state_desc  
  
 [sys.dm_hadr_availability_replica_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql)  
 返回一行以显示每个本地可用性副本的状态，并为同一可用性组中的每个远程可用性副本返回一行。  
  
 **列名：** replica_id、group_id、is_local、role、role_desc、operational_state、operational_state_desc、connected_state、connected_state_desc、recovery_health、recovery_health_desc、synchronization_health、synchronization_health_desc、last_connect_error_number、last_connect_error_description 和 last_connect_error_timestamp  
  
 [sys.fn_hadr_backup_is_preferred_replica](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)  
 确定当前副本是否为首选备份副本。  
  
> [!NOTE]  
>  有关可用性副本的性能计数器（ **SQLServer:Availability Replica**  性能对象）的信息，请参阅 [SQL Server，可用性副本](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)。  
  
##  <a name="AvDbs"></a>监视可用性数据库  
 若要监视可用性数据库，请使用以下视图：  
  
 [监视可用性数据库](/sql/relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql)  
 为 SQL Server 实例上的每个数据库（作为群集中所有 AlwaysOn 可用性组的一部分）包含一行，不论本地副本数据库是否联接到可用性组。  
  
> [!NOTE]  
>  将数据库添加到可用性组后，主数据库自动联接到该组。 必须在每个辅助副本上准备辅助数据库，之后才能将其联接到可用性组。  
  
 **列名：** group_id、group_database_id database_name  
  
 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
 为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例中的每个数据库都包含一行。 如果数据库属于某个可用性副本，该数据库对应的行将显示该副本的 GUID，以及该数据库在其可用性组中的唯一标识符。  
  
 列名： replica_id、group_database_id ** [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] **  
  
 [sys.dm_hadr_auto_page_repair](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql)  
 为针对任何可用性数据库（位于服务器实例为任何可用性组承载的可用性副本上）的每一个自动页修复尝试都返回一行。 该视图包含对应于给定主/辅助数据库上最新自动页修复尝试的行，每个数据库最多可对应 100 行。 只要一个数据库对应的行达到最大值，则它的下个自动页修复尝试对应的行将替换现有的一个项。  
  
 **列名：** database_id、file_id、page_id、error_type、page_status、modification_time  
  
 [sys.dm_hadr_database_replica_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql)  
 为参与任何可用性组（ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的本地实例正承载其可用性副本）的每个数据库返回一行。  
  
 **列名：** database_id、group_id、replica_id、group_database_id、is_local、synchronization_state、synchronization_state_desc、is_commit_participant、synchronization_health、synchronization_health_desc、database_state、database_state_desc、is_suspended、suspend_reason、suspend_reason_desc、recovery_lsn、truncation_lsn、last_sent_lsn、last_sent_time、last_received_lsn、last_received_time、last_hardened_lsn、last_hardened_time、last_redone_lsn、last_redone_time、log_send_queue_size、log_send_rate、redo_queue_size、redo_rate、filestream_send_rate、end_of_log_lsn、last_commit_lsn、last_commit_time、low_water_mark_for_ghosts  
  
 [sys.availability_databases_cluster](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql)  
 返回一行信息，这些信息旨在让您洞察 WSFC 故障转移群集 (WSFC) 群集上每个可用性组中的可用性数据库的运行状况。 此动态管理视图适用于以下情况：计划或响应某一故障转移，或发现可用性组中的哪一个辅助副本正在阻止给定主数据库上的日志截断。  
  
 **列名：** replica_id、group_database_id、database_name、is_failover_ready、is_pending_secondary_suspend、is_database_joined、recovery_lsn、truncation_lsn  
  
> [!NOTE]  
>  主副本位置是可用性组的权威来源。  
  
> [!NOTE]  
>  有关可用性数据库的 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 性能计数器（ **SQLServer:Database Replica** 性能对象）的信息，请参阅 [SQL Server，数据库副本](../../../relational-databases/performance-monitor/sql-server-database-replica.md)。 此外，若要监视可用性数据库上的事务日志活动，请使用以下 SQLServer 计数器 **：数据库**性能对象： "**日志刷新写入时间（毫秒）**"、"日志刷新次数/**秒**"、"日志**池缓存未命中数/秒**"、"**日志池磁盘读取次数/秒**" 和 "**日志池请求数/秒**"。有关详细信息，请参阅[SQL Server，数据库对象](../../../relational-databases/performance-monitor/sql-server-databases-object.md)。  
  
##  <a name="AGlisteners"></a>监视可用性组侦听器  
 若要监视 WSFC 群集子网上的可用性组侦听器，请使用以下视图：  
  
 [sys.availability_group_listener_ip_addresses](/sql/relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql)  
 针对可用性组侦听器，为当前联机的每个符合标准的虚拟 IP 地址返回一行。  
  
 **列名：** listener_id、ip_address、ip_subnet_mask、is_dhcp、network_subnet_ip、network_subnet_prefix_length、network_subnet_ipv4_mask、state、state_desc  
  
 [sys.availability_group_listeners](/sql/relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql)  
 对于给定的可用性组，返回零行（指示没有与该可用性组关联的网络名称），或为 WSFC 群集中的每个可用性组侦听器配置返回一行。  
  
 **列名：** group_id、listener_id、dns_name、port、is_conformant、ip_configuration_string_from_cluster  
  
 [sys.dm_tcp_listener_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql)  
 返回包含各个 TCP 侦听器的动态信息的行。  
  
 **列名：** listener_id、ip_address、is_ipv4、port、type、type_desc、state、state_desc、start_time  
  
 **主键：** listener_id  
  
 有关可用性组侦听程序的信息，请参阅[可用性组侦听程序、客户端连接和应用程序故障转移 (SQL Server)](../../listeners-client-connectivity-application-failover.md)。  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **AlwaysOn 可用性组监视任务：**  
  
-   [使用对象资源管理器详细信息来监视可用性组 &#40;SQL Server Management Studio&#41;](use-object-explorer-details-to-monitor-availability-groups.md)  
  
-   [查看可用性组属性 (SQL Server)](view-availability-group-properties-sql-server.md)  
  
-   [查看可用性副本属性 (SQL Server)](view-availability-replica-properties-sql-server.md)  
  
-   [查看可用性组侦听程序属性 (SQL Server)](view-availability-group-listener-properties-sql-server.md)  
  
 **AlwaysOn 可用性组监视参考 (Transact-SQL)：**  
  
-   [SERVERPROPERTY (Transact-SQL)](/sql/t-sql/functions/serverproperty-transact-sql)  
  
-   [sys. availability_group_listener_ip_addresses &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-availability-group-listener-ip-addresses-transact-sql)  
  
-   [sys. availability_group_listeners &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-availability-group-listeners-transact-sql)  
  
-   [sys. availability_databases_cluster &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-availability-databases-cluster-transact-sql)  
  
-   [sys. availability_groups &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-availability-groups-transact-sql)  
  
-   [sys. availability_read_only_routing_lists &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)  
  
-   [sys. availability_replicas &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)  
  
-   [sys. dm_hadr_availability_replica_cluster_nodes &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-nodes-transact-sql)  
  
-   [sys. dm_hadr_availability_replica_cluster_states &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql)  
  
-   [sys.database_mirroring_endpoints (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
-   [sys. dm_hadr_auto_page_repair &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql)  
  
-   [sys. dm_hadr_availability_group_states &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql)  
  
-   [sys. dm_hadr_availability_replica_cluster_states &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-cluster-states-transact-sql)  
  
-   [sys. dm_hadr_availability_replica_states &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql)  
  
-   [sys. dm_hadr_database_replica_states &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql)  
  
-   [sys. dm_hadr_database_replica_cluster_states &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql)  
  
-   [sys. dm_hadr_cluster &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql)  
  
-   [sys. dm_hadr_cluster_members &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql)  
  
-   [sys. dm_hadr_cluster_networks &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql)  
  
-   [sys. dm_hadr_database_replica_cluster_states &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql)  
  
-   [sys. dm_hadr_database_replica_states &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql)  
  
-   [sys. dm_hadr_instance_node_map &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-instance-node-map-transact-sql)  
  
-   [sys. dm_hadr_name_id_map &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-name-id-map-transact-sql)  
  
-   [sys. dm_os_performance_counters &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
-   [sys. dm_tcp_listener_states &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql)  
  
-   [sys. fn_hadr_backup_is_preferred_replica &#40;Transact-sql&#41;](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)  
  
 **AlwaysOn 性能计数器：**  
  
-   [SQL Server，可用性副本](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)  
  
-   [SQL Server，数据库副本](../../../relational-databases/performance-monitor/sql-server-database-replica.md)  
  
-   [SQL Server，Databases 对象](../../../relational-databases/performance-monitor/sql-server-databases-object.md)  
  
 **AlwaysOn 可用性组的基于策略的管理**  
  
-   [使用 AlwaysOn 策略查看可用性组的运行状况 &#40;SQL Server&#41;](use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
-   [使用 AlwaysOn 仪表板 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组（SQL Server）](always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [监视可用性组 &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
  
