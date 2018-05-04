---
title: sys.dm_hadr_cluster (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_cluster
- dm_hadr_cluster_HADR
- sys.dm_hadr_cluster_TSQL
- dm_hadr_cluster
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_cluster catalog view
- Availability Groups [SQL Server], WSFC clusters
ms.assetid: 13ce70e4-9d43-4a80-a826-099e6213bf85
caps.latest.revision: 20
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2f92cb181f422589b1b050e14cde4938ad013a1d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmhadrcluster-transact-sql"></a>sys.dm_hadr_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  如果 Windows Server 容錯移轉叢集 (WSFC) 節點所裝載的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]啟用[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]有 WSFC 仲裁， **sys.dm_hadr_cluster**傳回一個資料列會公開叢集名稱以及資訊有關此仲裁。 如果 WSFC 節點沒有仲裁，則不傳回任何資料列。  
 > [!TIP]
 > 從開始[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，這個動態管理檢視支援 Alwayson 容錯移轉叢集執行個體除了 Alwayson 可用性群組。

|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**cluster_name**|**nvarchar(128)**|WSFC 叢集的名稱，該叢集會裝載啟用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 執行個體。|  
|**quorum_type**|**tinyint**|這個 WSFC 叢集所使用的仲裁類型，可為下列其中一個值：<br /><br /> 0 = 節點多數。 此仲裁設定可維持一半節點的失敗數 (四捨五入) 減一。 例如，在七個節點的叢集上，這個仲裁設定可以維持三個節點失敗數。<br /><br /> 1 = 節點與磁碟多數。 如果磁碟見證依然在線上，此仲裁設定可維持一半節點的失敗數 (四捨五入)。 例如，如果在六個節點的叢集中，有磁碟見證處於線上，則可維持三個節點失敗數。 如果磁碟見證離線或失敗，此仲裁設定可維持一半節點的失敗數 (四捨五入) 減一。 例如，如果在六個節點的叢集中，有失敗的磁碟見證，則可維持兩個節點 (3-1=2) 失敗數。<br /><br /> 2 = 節點與檔案共用多數。 此仲裁設定的運作方式類似於「節點與磁碟多數」，但是會使用檔案共用見證，而非磁碟見證。<br /><br /> 3 = 無多數，僅限磁碟。 如果仲裁磁碟在線上，此仲裁設定可維持所有節點的失敗數，除了一以外。|  
|**quorum_type_desc**|**varchar(50)**|描述**quorum_type**，下列其中一個的：<br /><br /> NODE_MAJORITY<br /><br /> NODE_AND_DISK_MAJORITY<br /><br /> NODE_AND_FILE_SHARE_MAJORITY<br /><br /> NO_MAJORITY:_DISK_ONLY|  
|**quorum_state**|**tinyint**|WSFC 仲裁的狀態，下列其中一個值：<br /><br /> 0 = 未知仲裁狀態<br /><br /> 1 = 正常仲裁<br /><br /> 2 = 強制仲裁|  
|**quorum_state_desc**|**varchar(50)**|描述**quorum_state**，下列其中一個的：<br /><br /> UNKNOWN_QUORUM_STATE<br /><br /> NORMAL_QUORUM<br /><br /> FORCED_QUORUM|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組動態管理檢視和函式 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性群組目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [監視可用性群組 & #40;TRANSACT-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_hadr_cluster_members &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)  
  
  
