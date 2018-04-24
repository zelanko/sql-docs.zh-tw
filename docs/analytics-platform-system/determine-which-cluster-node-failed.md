---
title: 判斷失敗的叢集節點-Analytics Platform System |Microsoft 文件
description: 本文說明如何判斷 Analytics Platform System (APS) 節點失敗之後發生叢集容錯移轉，且已引發叢集容錯移轉警示的名稱。 疑難排解叢集容錯移轉的一部分，您必須決定無法再連絡 Microsoft，以協助解決問題的節點名稱。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 031c8033e91d7a7f74ca8c4409bc02296a22ebcf
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
---
# <a name="determine-which-cluster-node-failed-for-analytics-platform-system"></a>判斷哪一個叢集節點失敗 Analytics Platform System
本主題描述如何判斷 Analytics Platform System (APS) 節點失敗之後發生叢集容錯移轉，且已引發叢集容錯移轉警示的名稱。 疑難排解叢集容錯移轉的一部分，您必須決定無法再連絡 Microsoft，以協助解決問題的節點名稱。  
  
## <a name="Background"></a>背景  
SQL Server PDW 中的高可用性，控制節點和運算節點會設定為主動或被動 Windows 容錯移轉叢集的元件。 當作用中的伺服器無法回應重要的系統要求時，則被動伺服器容錯移轉，而執行失敗的伺服器功能。  
  
叢集容錯移轉之後，當 SQL Server PDW 報告節點狀態，則被動伺服器具有失敗狀態。 不過，看不出問題的伺服器或節點失敗，尤其是當失敗的伺服器仍在線上。 若要疑難排解叢集失敗，您必須判斷容錯移轉節點的名稱。  
  
## <a name="AdminConsoleSolution"></a>系統管理員主控台方案  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>若要尋找失敗的節點名稱  
  
1.  開啟系統管理員主控台。 如需系統管理員主控台的詳細資訊，請參閱[使用管理主控台來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)。 發生容錯移轉之後，容錯移轉事件是否包含在警示數目上**健全狀況**頁面。 沒有**健全狀況**PDW 區域，HDI 區域中，與設備的網狀架構區域的頁面。 每個健全狀況 頁面具有**警示** 索引標籤。若要深入了解警示，按一下健全狀況 頁面的 警示 索引標籤，然後按一下警示。  
  
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
  
