---
title: sys.dm_hadr_cluster_members (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/31/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e19451a24d35e63fa84a17d409d19b5c9b02ccc3
ms.sourcegitcommit: 7c052fc969d0f2c99ad574f99076dc1200d118c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2019
ms.locfileid: "55570721"
---
# <a name="sysdmhadrclustermembers-transact-sql"></a>sys.dm_hadr_cluster_members (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  如果裝載已啟用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 本機執行個體的 WSFC 節點有 WSFC 仲裁，則針對構成仲裁的每個成員及其狀態各傳回一個資料列。 這包括所有叢集中的節點 (與 CLUSTER_ENUM_NODE 型別傳回**Clusterenum**函式) 與磁碟或檔案共用見證，如果有的話。 針對給定成員傳回的資料列包含有關該成員之狀態的資訊。 比方說，針對多數節點仲裁，在其中一個節點已關閉時的五個節點叢集**sys.dm_hadr_cluster_members**的伺服器執行個體啟用查詢[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]位於仲裁，某個節點上**sys.dm_hadr_cluster_members**會反映為"NODE_DOWN"將關閉節點的狀態。  
  
 如果 WSFC 節點沒有仲裁，則不傳回任何資料列。  
  
 使用這個動態管理檢視可回答下列問題：  
  
-   哪些節點目前正在 WSFC 叢集上執行？  
  
-   WSFC 叢集在遺失 majority-node 案例中的仲裁之前，還可容忍其他多少失敗？  

 > [!TIP]
 > 從開始[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，此動態管理檢視支援 Alwayson 容錯移轉叢集執行個體除了 Always On 可用性群組。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|成員名稱，這可以是電腦名稱、磁碟機代號或檔案共用路徑。|  
|**member_type**|**tinyint**|成員的類型，可為下列其中一個值：<br /><br /> 0 = WSFC 節點<br /><br /> 1 = 磁碟見證<br /><br /> 2 = 檔案共用見證<br /><br /> 3 = 雲端見證|  
|**member_type_desc**|**nvarchar(50)**|Popis **member_type**，下列其中一個的：<br /><br /> CLUSTER_NODE<br /><br /> DISK_WITNESS<br /><br /> FILE_SHARE_WITNESS<br /><br /> CLOUD_WITNESS|  
|**member_state**|**tinyint**|成員狀態，可為下列其中一個值：<br /><br /> 0 = 離線<br /><br /> 1 = 線上|  
|**member_state_desc**|**nvarchar(60)**|Popis **member_state**，下列其中一個的：<br /><br /> UP<br /><br /> 向下|  
|**number_of_quorum_votes**|**tinyint**|此仲裁成員擁有的仲裁投票數。 無多數：只有仲裁磁碟，這個值預設為 0。 如果是其他仲裁類型，這個值預設為 1。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="examples"></a>範例  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組動態管理檢視和函式 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性群組目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [監視可用性群組 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性群組&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
