---
title: "sys.dm_os_cluster_properties (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_cluster_properties_TSQL
- sys.dm_os_cluster_properties
- dm_os_cluster_properties_TSQL
- dm_os_cluster_properties
dev_langs:
- TSQL
helpviewer_keywords:
- dm_os_cluster_properties
- sys.dm_os_cluster_properties
ms.assetid: 6d82e770-fba7-49e0-9a0c-3b34b393e4a7
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 71ac8027fa835a1d087c9914b73b8a1e4c0ead34
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmosclusterproperties-transact-sql"></a>sys.dm_os_cluster_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回一個資料列，並在其中包含本主題所指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 叢集資源屬性的目前設定。 如果在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 獨立執行個體上執行此檢視，將不會傳回資料。  
  
 這些屬性可用於設定影響失敗偵測、失敗回應時間，以及監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體健全狀態之記錄的值。  
  

|資料行名稱|屬性|Description|  
|-----------------|--------------|-----------------|  
|VerboseLogging|bigint|SQL Server 容錯移轉叢集的記錄層次。 可開啟以在錯誤記錄檔中提供詳細資訊供疑難排解之用的詳細資訊記錄。 為下列其中一個值：<br /><br /> 0 - 關閉記錄功能 (預設)<br /><br /> 1 - 只有錯誤<br /><br /> 2 - 錯誤和警告<br /><br /> 如需詳細資訊，請參閱[ALTER SERVER CONFIGURATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md).|  
|SqlDumperDumpFlags|bigint|SQLDumper 傾印旗標決定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所產生的傾印檔案類型。 預設設定為 0。|  
|SqlDumperDumpPath|nvarchar(260)|SQLDumper 公用程式產生傾印檔案的位置。|  
|SqlDumperDumpTimeOut|bigint|當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發生失敗時，SQLDumper 公用程式產生傾印的逾時值 (以毫秒為單位)。 預設值是 0。|  
|FailureConditionLevel|bigint|設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集應該失敗或重新啟動的條件。 預設值是 3。 如需詳細說明，或變更的屬性設定，請參閱[Configure FailureConditionLevel Property Settings](../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md)。|  
|HealthCheckTimeout|bigint|SQL Server Database Engine 資源 DLL 在將 SQL Server 執行個體視為無回應之前，應該等候伺服器健全狀態資訊多久時間的逾時值。 逾時值以毫秒格式表示。 預設值為 60000。 如需詳細資訊，或變更這個屬性設定，請參閱[Configure HealthCheckTimeout Property Settings](../../sql-server/failover-clusters/windows/configure-healthchecktimeout-property-settings.md)。|  
  
## <a name="permissions"></a>Permissions  
 需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體的 VIEW SERVER STATE 權限。  
  
## <a name="examples"></a>範例  
 下列範例會使用 sys.dm_os_cluster_properties 傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集資源的屬性設定。  
  
```  
SELECT VerboseLogging, SqlDumperDumpFlags, SqlDumperDumpPath, SqlDumperDumpTimeOut, FailureConditionLevel, HealthCheckTimeout  
FROM sys.dm_os_cluster_properties;  
```  
  
 範例結果集如下：  
  
|VerboseLogging|SqlDumperDumpFlags|SqlDumperDumpPath|SqlDumperDumpTimeOut|FailureConditionLevel|HealthCheckTimeout|  
|--------------------|------------------------|-----------------------|--------------------------|---------------------------|------------------------|  
|0|0|NULL|0|3|60000|  
  
  
