---
title: 判斷失敗的叢集節點
description: 本文說明如何判斷在叢集容錯移轉發生後失敗的分析平臺系統（AP）節點名稱，並引發叢集容錯移轉警示。 在疑難排解叢集容錯移轉的過程中，您必須先判斷失敗的節點名稱，再聯繫 Microsoft 以協助解決問題。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 68ebdb7f17ddee311644e11c48eaa4b586beac74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401201"
---
# <a name="determine-which-cluster-node-failed-for-analytics-platform-system"></a>判斷分析平臺系統的哪個叢集節點失敗
本主題說明如何判斷在叢集容錯移轉發生之後失敗的分析平臺系統（AP）節點名稱，並引發叢集容錯移轉警示。 在疑難排解叢集容錯移轉的過程中，您必須先判斷失敗的節點名稱，再聯繫 Microsoft 以協助解決問題。  
  
## <a name="Background"></a>背景  
為了 SQL Server PDW 中的高可用性，控制節點和計算節點會設定為 Windows 容錯移轉叢集的主動或被動元件。 當作用中伺服器無法回應重要的系統要求時，被動伺服器會容錯回復，並執行失敗之伺服器的功能。  
  
叢集容錯移轉之後，當 SQL Server PDW 報告節點狀態時，被動伺服器的狀態會是 [已容錯移轉]。 不過，這並不明顯地是哪個伺服器或節點失敗，特別是當失敗的伺服器仍在線上時。 若要針對叢集失敗進行疑難排解，您必須判斷故障切換的節點名稱。  
  
## <a name="AdminConsoleSolution"></a>管理主控台解決方案  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>若要尋找失敗的節點名稱  
  
1.  開啟管理主控台。 如需管理主控台的詳細資訊，請參閱[使用管理主控台監視設備 &#40;分析平臺系統&#41;](monitor-the-appliance-by-using-the-admin-console.md)。 發生容錯移轉之後，容錯移轉事件就會包含在 [**健全狀況**] 頁面上的警示數目中。 有一個適用于 PDW 區域的**健康**情況頁面，以及設備的網狀架構區域。 每個健全狀況頁面都有 [**警示**] 索引標籤。若要深入瞭解警示，請按一下 [健康情況] 頁面、[警示] 索引標籤，然後按一下警示。  
  
## <a name="SystemView"></a>系統檢視解決方案  
下列 SQL 語句顯示如何使用[sys.databases dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)系統檢視來尋找失敗的伺服器名稱。  
  
```sql  
SELECT  
SUBSTRING( component_instance_id, 2, charindex(' ', component_instance_id, 1)-2) AS failed_node_name,  
create_time AS failover_time  
FROM sys.dm_pdw_component_health_active_alerts  
WHERE alert_id = 500139  
ORDER BY failed_node_name;  
```  
  
