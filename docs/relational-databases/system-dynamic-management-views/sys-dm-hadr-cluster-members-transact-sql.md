---
title: sys.databases dm_hadr_cluster_members （Transact-sql） |Microsoft Docs
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8b28b708aabfdf3ec4e569aab6d8a95e2330b370
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67900760"
---
# <a name="sysdm_hadr_cluster_members-transact-sql"></a>sys.dm_hadr_cluster_members (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  如果裝載已啟用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 本機執行個體的 WSFC 節點有 WSFC 仲裁，則針對構成仲裁的每個成員及其狀態各傳回一個資料列。 這包括叢集中的所有節點（以**Clusterenum**函式所傳回的 CLUSTER_ENUM_NODE 類型）和磁片或檔案共用見證（如果有的話）。 針對給定成員傳回的資料列包含有關該成員之狀態的資訊。 例如，對於具有多數節點仲裁（其中一個節點已關閉）的五個節點叢集，當**sys. dm_hadr_cluster_members**是從已啟用[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]的伺服器實例進行查詢，而該實例是在具有仲裁的節點上，則**dm_hadr_cluster_members**會將下節點的狀態反映為 "NODE_DOWN"。  
  
 如果 WSFC 節點沒有仲裁，則不傳回任何資料列。  
  
 使用這個動態管理檢視可回答下列問題：  
  
-   哪些節點目前正在 WSFC 叢集上執行？  
  
-   WSFC 叢集在遺失 majority-node 案例中的仲裁之前，還可容忍其他多少失敗？  

 > [!TIP]
 > 從開始[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，這個動態管理檢視除了 Always On 可用性群組之外，還支援 Always On 容錯移轉叢集實例。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|成員名稱，這可以是電腦名稱、磁碟機代號或檔案共用路徑。|  
|**member_type**|**tinyint**|成員的類型，可為下列其中一個值：<br /><br /> 0 = WSFC 節點<br /><br /> 1 = 磁碟見證<br /><br /> 2 = 檔案共用見證<br /><br /> 3 = 雲端見證|  
|**member_type_desc**|**nvarchar(50)**|**Member_type**的描述，下列其中一個：<br /><br /> CLUSTER_NODE<br /><br /> DISK_WITNESS<br /><br /> FILE_SHARE_WITNESS<br /><br /> CLOUD_WITNESS|  
|**member_state**|**tinyint**|成員狀態，可為下列其中一個值：<br /><br /> 0 = 離線<br /><br /> 1 = 線上|  
|**member_state_desc**|**nvarchar(60)**|**Member_state**的描述，下列其中一個：<br /><br /> UP<br /><br /> DOWN|  
|**number_of_quorum_votes**|**tinyint**|此仲裁成員擁有的仲裁投票數。 如果是「無多數：僅限磁碟」的仲裁，這個值預設為 0。 如果是其他仲裁類型，這個值預設為 1。|  
  
## <a name="permissions"></a>權限  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="examples"></a>範例  
  
## <a name="see-also"></a>另請參閱  
 [Always On 可用性群組動態管理檢視和函數 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Always On 可用性群組目錄檢視 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [&#40;Transact-sql&#41;監視可用性群組](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
