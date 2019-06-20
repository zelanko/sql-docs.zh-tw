---
title: 判斷失敗的叢集節點-Analytics Platform System |Microsoft Docs
description: 本文說明如何判斷失敗發生叢集容錯移轉後已發出叢集容錯移轉警示 Analytics Platform System (APS) 節點的名稱。 疑難排解叢集容錯移轉的一部分，您必須判斷連絡 Microsoft，以協助解決此問題之前失敗的節點名稱。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4fd739e55725a3138a22539ef837088f86c8d8b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63283149"
---
# <a name="determine-which-cluster-node-failed-for-analytics-platform-system"></a>判斷哪一個叢集節點失敗 Analytics Platform System
本主題描述如何判斷失敗發生叢集容錯移轉後已發出叢集容錯移轉警示 Analytics Platform System (APS) 節點的名稱。 疑難排解叢集容錯移轉的一部分，您必須判斷連絡 Microsoft，以協助解決此問題之前失敗的節點名稱。  
  
## <a name="Background"></a>背景  
SQL Server PDW 中的高可用性，控制節點和計算節點會設定為主動或被動 Windows 容錯移轉叢集的元件。 當作用中的伺服器無法回應重要的系統要求時，則被動伺服器容錯移轉，而執行失敗的伺服器功能。  
  
叢集容錯移轉之後，當 SQL Server PDW 報告節點狀態，則被動伺服器高於失敗狀態。 不過，它並不明顯的伺服器或節點失敗，尤其是如果失敗的伺服器仍在線上。 若要疑難排解叢集失敗的狀況，您必須決定容錯移轉節點的名稱。  
  
## <a name="AdminConsoleSolution"></a>系統管理員主控台的解決方案  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>若要尋找失敗的節點名稱  
  
1.  開啟 [系統管理員主控台]。 如需有關系統管理員主控台的詳細資訊，請參閱[使用管理主控台來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)。 發生容錯移轉之後，容錯移轉事件是否包含在警示數目上**健全狀況**頁面。 沒有**健全狀況**PDW 區域和設備的網狀架構區域的頁面。 每個健康情況頁面都**警示** 索引標籤。若要深入了解警示，按一下健全狀況 頁面的 警示 索引標籤，然後按一下警示。  
  
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
  
