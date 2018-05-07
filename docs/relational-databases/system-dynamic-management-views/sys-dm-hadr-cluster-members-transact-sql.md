---
title: sys.dm_hadr_cluster_members (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 01/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_cluster_members_TSQL
- sys.dm_hadr_cluster_members
- dm_hadr_cluster_members_TSQL
- dm_hadr_cluster_members
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_cluster_members catalog view
ms.assetid: feb20b3a-8835-41d3-9a1c-91d3117bc170
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 80c34e7002ffb53239e62492d98eb9ba5ce631ba
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmhadrclustermembers-transact-sql"></a>sys.dm_hadr_cluster_members (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  如果裝載已啟用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 本機執行個體的 WSFC 節點有 WSFC 仲裁，則針對構成仲裁的每個成員及其狀態各傳回一個資料列。 這包括所有叢集中的節點 (與 CLUSTER_ENUM_NODE 型別，傳回**Clusterenum**函式)，如果有任何的磁碟或檔案共用見證。 針對給定成員傳回的資料列包含有關該成員之狀態的資訊。 例如，針對多數節點仲裁，在其中一個節點已關閉時的五個節點叢集**sys.dm_hadr_cluster_members**查詢從伺服器執行個體是針對啟用[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]位於仲裁，某個節點上**sys.dm_hadr_cluster_members**會反映為"NODE_DOWN"將關閉節點的狀態。  
  
 如果 WSFC 節點沒有仲裁，則不傳回任何資料列。  
  
 使用這個動態管理檢視可回答下列問題：  
  
-   哪些節點目前正在 WSFC 叢集上執行？  
  
-   WSFC 叢集在遺失 majority-node 案例中的仲裁之前，還可容忍其他多少失敗？  

 > [!TIP]
 > 從開始[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，這個動態管理檢視支援 Alwayson 容錯移轉叢集執行個體除了 Alwayson 可用性群組。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|成員名稱，這可以是電腦名稱、磁碟機代號或檔案共用路徑。|  
|**member_type**|**tinyint**|成員的類型，可為下列其中一個值：<br /><br /> 0 = WSFC 節點<br /><br /> 1 = 磁碟見證<br /><br /> 2 = 檔案共用見證|  
|**member_type_desc**|**nvarchar(50)**|描述**member_type**，下列其中一個的：<br /><br /> CLUSTER_NODE<br /><br /> DISK_WITNESS<br /><br /> FILE_SHARE_WITNESS|  
|**member_state**|**tinyint**|成員狀態，可為下列其中一個值：<br /><br /> 0 = 離線<br /><br /> 1 = 線上|  
|**member_state_desc**|**nvarchar(60)**|描述**member_state**，下列其中一個的：<br /><br /> UP<br /><br /> 向下|  
|**number_of_quorum_votes**|**tinyint**|此仲裁成員擁有的仲裁投票數。 如果是「無多數：僅限磁碟」的仲裁，這個值預設為 0。 如果是其他仲裁類型，這個值預設為 1。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="examples"></a>範例  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組動態管理檢視和函式 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性群組目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [監視可用性群組 & #40;TRANSACT-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性群組 & #40;SQL Server & #41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
