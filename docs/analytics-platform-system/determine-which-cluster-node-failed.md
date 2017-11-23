---
title: "判斷哪一個叢集節點失敗 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e001117-a1b6-4357-bf25-e85aba3f1cf0
caps.latest.revision: "21"
ms.openlocfilehash: 59f188526cff2d605c5bffcf2187b3c765276c81
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="determine-which-cluster-node-failed"></a>判斷哪一個叢集節點失敗
本主題描述如何判斷 SQL Server PDW 節點失敗之後發生叢集容錯移轉，且已引發叢集容錯移轉警示的名稱。 疑難排解叢集容錯移轉的一部分，您必須決定無法再連絡 Microsoft，以協助解決問題的節點名稱。  
  
## <a name="Background"></a>背景  
SQL Server PDW 中的高可用性，控制節點和運算節點會設定為主動或被動 Windows 容錯移轉叢集的元件。 當作用中的伺服器無法回應重要的系統要求時，則被動伺服器容錯移轉，而執行失敗的伺服器功能。  
  
叢集容錯移轉之後，當 SQL Server PDW 報告節點狀態，則被動伺服器具有失敗狀態。 不過，看不出問題的伺服器或節點失敗，尤其是當失敗的伺服器仍在線上。 若要疑難排解叢集失敗，您必須判斷容錯移轉節點的名稱。  
  
## <a name="AdminConsoleSolution"></a>系統管理員主控台方案  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>若要尋找失敗的節點名稱  
  
1.  開啟系統管理員主控台。 如需系統管理員主控台的詳細資訊，請參閱[使用系統管理員主控台 &#40; 監視的應用裝置Analytics Platform System &#41;](monitor-the-appliance-by-using-the-admin-console.md). 發生容錯移轉之後，容錯移轉事件是否包含在警示數目上**健全狀況**頁面。 沒有**健全狀況**PDW 區域，HDI 區域中，與設備的網狀架構區域的頁面。 每個健全狀況 頁面具有**警示** 索引標籤。若要深入了解警示，按一下健全狀況 頁面的 警示 索引標籤，然後按一下警示。  
  
## <a name="SystemView"></a>系統檢視解決方案  
下列 SQL 陳述式示範如何使用[sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)系統檢視表來尋找失敗的伺服器名稱。  
  
```sql  
SELECT  
SUBSTRING( component_instance_id, 2, charindex(' ', component_instance_id, 1)-2) AS failed_node_name,  
create_time AS failover_time  
FROM sys.dm_pdw_component_health_active_alerts  
WHERE alert_id = 500139  
ORDER BY failed_node_name;  
```  
  
