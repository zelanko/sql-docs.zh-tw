---
title: "複寫資料表 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: TSQL
helpviewer_keywords:
- system tables [SQL Server], replication
- replication [SQL Server], system tables
ms.assetid: 5696ee73-5d7c-4f26-b7ee-6831c9c3edf7
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: da1d0ec4572c89ace6dd0849228842611822d60d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="replication-tables-transact-sql"></a>複寫資料表 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  複寫拓撲是由複寫系統資料表所支援。 當使用者資料庫被設定為發行者或訂閱者時，複寫便會將系統資料表加入資料庫中。 當使用者資料庫從複寫拓撲中移除時，也會一併移除這些資料表。 一般規則有關使用系統資料表，請參閱[系統資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md).  
  
## <a name="replication-tables"></a>複寫資料表  
 下列是複寫所用的系統資料表清單，這些系統資料表是根據資料庫加以分組。  
  
### <a name="replication-tables-in-the-master-database"></a>master 資料庫中的複寫資料表  
  
|||  
|-|-|  
|[MSreplication_options &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/msreplication-options-transact-sql.md)||  
  
### <a name="replication-tables-in-the-msdb-database"></a>msdb 資料庫中的複寫資料表  
  
|||  
|-|-|  
|[MSagentparameterlist](../../relational-databases/system-tables/msagentparameterlist-transact-sql.md)|[MSdbms_map](../../relational-databases/system-tables/msdbms-map-transact-sql.md)|  
|[MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md)|[MSreplmonthresholdmetrics](../../relational-databases/system-tables/msreplmonthresholdmetrics-transact-sql.md)|  
|[MSdbms_datatype](../../relational-databases/system-tables/msdbms-datatype-transact-sql.md)|[sysreplicationalerts](../../relational-databases/system-tables/sysreplicationalerts-transact-sql.md)|  
|[MSdbms_datatype_mapping](../../relational-databases/system-tables/msdbms-datatype-mapping-transact-sql.md)||  
  
### <a name="replication-tables-in-the-distribution-database"></a>散發資料庫中的複寫資料表  
  
|||  
|-|-|  
|[MSagent_parameters](../../relational-databases/system-tables/msagent-parameters-transact-sql.md)|[MSpublicationthresholds](../../relational-databases/system-tables/mspublicationthresholds-transact-sql.md)|  
|[MSagent_profiles](../../relational-databases/system-tables/msagent-profiles-transact-sql.md)|[MSpublisher_databases](../../relational-databases/system-tables/mspublisher-databases-transact-sql.md)|  
|[MSarticles](../../relational-databases/system-tables/msarticles-transact-sql.md)|[MSreplication_objects](../../relational-databases/system-tables/msreplication-objects-transact-sql.md)|  
|[MScached_peer_lsns](../../relational-databases/system-tables/mscached-peer-lsns-transact-sql.md)|[MSreplication_subscriptions](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)|  
|[MSdistpublishers](../../relational-databases/system-tables/msdistpublishers-transact-sql.md)|[MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md)|  
|[MSdistribution_agents](../../relational-databases/system-tables/msdistribution-agents-transact-sql.md)|[MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md)|  
|[MSdistribution_history](../../relational-databases/system-tables/msdistribution-history-transact-sql.md)|[MSrepl_originators](../../relational-databases/system-tables/msrepl-originators-transact-sql.md)|  
|[MSdistributiondbs](../../relational-databases/system-tables/msdistributiondbs-transact-sql.md)|[MSrepl_transactions](../../relational-databases/system-tables/msrepl-transactions-transact-sql.md)|  
|[MSdistributor](../../relational-databases/system-tables/msdistributor-transact-sql.md)|[MSrepl_version](../../relational-databases/system-tables/msrepl-version-transact-sql.md)|  
|[MSlogreader_agents](../../relational-databases/system-tables/mslogreader-agents-transact-sql.md)|[MSsnapshot_agents](../../relational-databases/system-tables/mssnapshot-agents-transact-sql.md)|  
|[MSlogreader_history](../../relational-databases/system-tables/mslogreader-history-transact-sql.md)|[MSsnapshot_history](../../relational-databases/system-tables/mssnapshot-history-transact-sql.md)|  
|[MSmerge_agents](../../relational-databases/system-tables/msmerge-agents-transact-sql.md)|[MSsubscriber_info](../../relational-databases/system-tables/mssubscriber-info-transact-sql.md)|  
|[MSmerge_history](../../relational-databases/system-tables/msmerge-history-transact-sql.md)|[MSsubscriber_schedule](../../relational-databases/system-tables/mssubscriber-schedule-transact-sql.md)|  
|[MSmerge_sessions](../../relational-databases/system-tables/msmerge-sessions-transact-sql.md)|[MSsubscriptions](../../relational-databases/system-tables/mssubscriptions-transact-sql.md)|  
|[MSmerge_subscriptions](../../relational-databases/system-tables/msmerge-subscriptions-transact-sql.md)|[MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)|  
|[MSpublication_access](../../relational-databases/system-tables/mspublication-access-transact-sql.md)|[MStracer_history](../../relational-databases/system-tables/mstracer-history-transact-sql.md)|  
|[MSpublications](../../relational-databases/system-tables/mspublications-transact-sql.md)|[MStracer_tokens](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md)|  
  
 散發資料庫中的這些資料表用於複寫非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者中的資料。 如需詳細資訊，請參閱[非 SQL Server 發行者](../../relational-databases/replication/non-sql/non-sql-server-publishers.md)。  
  
|||  
|-|-|  
|[IHarticles](../../relational-databases/system-tables/iharticles-transact-sql.md)|[IHpublishercolumnindexes](../../relational-databases/system-tables/ihpublishercolumnindexes-transact-sql.md)|  
|[IHcolumns](../../relational-databases/system-tables/ihcolumns-transact-sql.md)|[IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)|  
|[IHconstrainttypes](../../relational-databases/system-tables/ihconstrainttypes-transact-sql.md)|[IHpublisherconstraints](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md)|  
|[IHindextypes](../../relational-databases/system-tables/ihindextypes-transact-sql.md)|[IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md)|  
|[IHindextypes](../../relational-databases/system-tables/ihindextypes-transact-sql.md)|[IHpublishers](../../relational-databases/system-tables/ihpublishers-transact-sql.md)|  
|[IHpublications](../../relational-databases/system-tables/ihpublications-transact-sql.md)|[IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md)|  
|[IHpublishercolumnconstraints](../../relational-databases/system-tables/ihpublishercolumnconstraints-transact-sql.md)|[IHsubscriptions](../../relational-databases/system-tables/ihsubscriptions-transact-sql.md)|  
  
### <a name="replication-tables-in-the-publication-database"></a>發行集資料庫中的複寫資料表  
  
|||  
|-|-|  
|[conflict_\<結構描述 > _\<資料表 >](../../relational-databases/system-tables/conflict-schema-table-transact-sql.md)|[MSpeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md)|  
|[MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md)|[MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md)|  
|[MSdynamicsnapshotviews](../../relational-databases/system-tables/msdynamicsnapshotviews-transact-sql.md)|[MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md)|  
|[MSmerge_altsyncpartners](../../relational-databases/system-tables/msmerge-altsyncpartners-transact-sql.md)|[MSpeer_request](../../relational-databases/system-tables/mspeer-request-transact-sql.md)|  
|[MSmerge_conflicts_info](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)|[MSpeer_response](../../relational-databases/system-tables/mspeer-response-transact-sql.md)|  
|[MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)|[MSpub_identity_range](../../relational-databases/system-tables/mspub-identity-range-transact-sql.md)|  
|[MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md)|[sysarticlecolumns](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)|  
|[MSmerge_dynamic_snapshots](../../relational-databases/system-tables/msmerge-dynamic-snapshots-transact-sql.md)|[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)|  
|[MSmerge_errorlineage](../../relational-databases/system-tables/msmerge-errorlineage-transact-sql.md)|[sysarticleupdates](../../relational-databases/system-tables/sysarticleupdates-transact-sql.md)|  
|[MSmerge_generation_partition_mappings](../../relational-databases/system-tables/msmerge-generation-partition-mappings-transact-sql.md)|[sysmergearticlecolumns](../../relational-databases/system-tables/sysmergearticlecolumns-transact-sql.md)|  
|[MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)|[sysmergearticles](../../relational-databases/system-tables/sysmergearticles-transact-sql.md)|  
|[MSmerge_identity_range](../../relational-databases/system-tables/msmerge-identity-range-transact-sql.md)|[sysmergepartitioninfo](../../relational-databases/system-tables/sysmergepartitioninfo-transact-sql.md)|  
|[MSmerge_metadataaction_request](../../relational-databases/system-tables/msmerge-metadataaction-request-transact-sql.md)|[sysmergepublications](../../relational-databases/system-tables/sysmergepublications-transact-sql.md)|  
|[MSmerge_partition_groups](../../relational-databases/system-tables/msmerge-partition-groups-transact-sql.md)|[sysmergeschemaarticles](../../relational-databases/system-tables/sysmergeschemaarticles-transact-sql.md)|  
|[MSmerge_past_partition_mappings](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)|[sysmergeschemachange](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)|  
|[MSmerge_replinfo](../../relational-databases/system-tables/msmerge-replinfo-transact-sql.md)|[sysmergesubscriptions](../../relational-databases/system-tables/sysmergesubscriptions-transact-sql.md)|  
|[MSmerge_settingshistory](../../relational-databases/system-tables/msmerge-settingshistory-transact-sql.md)|[sysmergesubsetfilters](../../relational-databases/system-tables/sysmergesubsetfilters-transact-sql.md)|  
|[MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)|[syspublications](../../relational-databases/system-tables/syspublications-transact-sql.md)|  
|[MSpeer_conflictdetectionconfigrequest](../../relational-databases/system-tables/mspeer-conflictdetectionconfigrequest-transact-sql.md)|[sysschemaarticles](../../relational-databases/system-tables/sysschemaarticles-transact-sql.md)|  
|[MSpeer_conflictdetectionconfigresponse](../../relational-databases/system-tables/mspeer-conflictdetectionconfigresponse-transact-sql.md)|[syssubscriptions](../../relational-databases/system-tables/syssubscriptions-transact-sql.md)|  
|[MSpeer_lsns](../../relational-databases/system-tables/mspeer-lsns-transact-sql.md)|[systranschemas](../../relational-databases/system-views/systranschemas-transact-sql.md)|  
  
### <a name="replication-tables-in-the-subscription-database"></a>訂閱資料庫中的複寫資料表  
  
|||  
|-|-|  
|[MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md)|[MSmerge_settingshistory](../../relational-databases/system-tables/msmerge-settingshistory-transact-sql.md)|  
|[MSdynamicsnapshotviews](../../relational-databases/system-tables/msdynamicsnapshotviews-transact-sql.md)|[MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)|  
|[MSmerge_altsyncpartners](../../relational-databases/system-tables/msmerge-altsyncpartners-transact-sql.md)|[MSpeer_lsns &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/mspeer-lsns-transact-sql.md)|  
|[MSmerge_conflicts_info](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)|[MSrepl_queuedtraninfo](../../relational-databases/system-tables/msrepl-queuedtraninfo-transact-sql.md)|  
|[MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)|[MSsnapshotdeliveryprogress](../../relational-databases/system-tables/mssnapshotdeliveryprogress-transact-sql.md)|  
|[MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md)|[MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)|  
|[MSmerge_dynamic_snapshots](../../relational-databases/system-tables/msmerge-dynamic-snapshots-transact-sql.md)|[sysmergearticlecolumns](../../relational-databases/system-tables/sysmergearticlecolumns-transact-sql.md)|  
|[MSmerge_errorlineage](../../relational-databases/system-tables/msmerge-errorlineage-transact-sql.md)|[sysmergearticles](../../relational-databases/system-tables/sysmergearticles-transact-sql.md)|  
|[MSmerge_generation_partition_mappings](../../relational-databases/system-tables/msmerge-generation-partition-mappings-transact-sql.md)|[sysmergepartitioninfo](../../relational-databases/system-tables/sysmergepartitioninfo-transact-sql.md)|  
|[MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)|[sysmergepublications](../../relational-databases/system-tables/sysmergepublications-transact-sql.md)|  
|[MSmerge_identity_range](../../relational-databases/system-tables/msmerge-identity-range-transact-sql.md)|[sysmergeschemaarticles](../../relational-databases/system-tables/sysmergeschemaarticles-transact-sql.md)|  
|[MSmerge_metadataaction_request](../../relational-databases/system-tables/msmerge-metadataaction-request-transact-sql.md)|[sysmergeschemachange](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)|  
|[MSmerge_partition_groups](../../relational-databases/system-tables/msmerge-partition-groups-transact-sql.md)|[sysmergesubscriptions](../../relational-databases/system-tables/sysmergesubscriptions-transact-sql.md)|  
|[MSmerge_past_partition_mappings](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)|[sysmergesubsetfilters](../../relational-databases/system-tables/sysmergesubsetfilters-transact-sql.md)|  
|[MSmerge_replinfo](../../relational-databases/system-tables/msmerge-replinfo-transact-sql.md)|[systranschemas](../../relational-databases/system-views/systranschemas-transact-sql.md)|  
  
## <a name="see-also"></a>請參閱＜  
 [設定發行和散發](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [停用發行和散發](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
