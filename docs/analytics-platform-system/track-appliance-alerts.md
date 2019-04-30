---
title: 追蹤設備警示-Analytics Platform System |Microsoft Docs
description: 追蹤設備警示，Analytics Platform System 中。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f38f76975290538a35203ddbbed84b9354285edc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156998"
---
# <a name="track-appliance-alerts-in-analytics-platform-system"></a>Analytics Platform System 中的追蹤設備警示
本主題說明如何使用管理主控台和系統檢視表來追蹤 SQL Server PDW 應用裝置中的警示。  
  
## <a name="to-track-appliance-alerts"></a>若要追蹤設備警示  
SQL Server PDW 中，會建立需要注意的硬體和軟體問題的警示。 每個警示會包含標題和問題的描述。  
  
SQL Server PDW 中的記錄警示[sys.dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md) DMV。 系統會保留限制為 10,000 的警示，並超過限制時，先刪除最舊的警示。  
  
### <a name="view-alerts-by-using-the-admin-console"></a>使用管理主控台檢視警示  
沒有**警示**PDW 區域和設備的網狀架構區域 索引標籤。 發生容錯移轉之後，容錯移轉事件包含在頁面上的警示數目。 沒有頁面的 PDW 區域和設備的網狀架構區域。 每個健全狀況] 頁面有一個索引標籤。若要深入了解警示，按一下**健全狀況**頁面上，**警示**索引標籤，然後再按一下 [警示。  
  
![PDW 管理主控台警示](./media/track-appliance-alerts/SQL_Server_PDW_AdminConsole_AlertsV2.png "SQL_Server_PDW_AdminConsole_AlertsV2")  
  
在 **警示**頁面：  
  
-   若要檢視警示的歷程記錄，請按一下**檢閱警示歷程記錄**連結。  
  
-   若要檢視警示的元件和其目前的屬性值，請按一下警示的資料列。  
  
-   若要檢視有關引發警示的節點詳細資料，請按一下節點名稱。  
  
### <a name="view-alerts-by-using-the-system-views"></a>使用系統檢視表的檢視警示  
若要使用系統檢視表中檢視警示，請查詢[sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)。 此 DMV 會顯示未更正的警示。 分級的警示和錯誤的說明，請使用[sys.dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md) DMV。  
  
下列範例是常用的查詢，來檢視目前的警示。  
  
```sql  
SELECT   
    aa.[pdw_node_id],  
    n.[name] AS [node_name],  
    g.[group_name] ,  
    c.[component_name] ,  
    aa.[component_instance_id] ,   
    a.[alert_name] ,  
    a.[state] ,  
    a.[severity] ,  
    aa.[current_value] ,  
    aa.[previous_value] ,  
    aa.[create_time] ,  
    a.[description]   
FROM [sys].[dm_pdw_component_health_active_alerts] AS aa  
    INNER JOIN sys.dm_pdw_nodes AS n   
        ON aa.[pdw_node_id] = n.[pdw_node_id]  
    INNER JOIN [sys].[pdw_health_components] AS c   
        ON aa.[component_id] = c.[component_id]  
    INNER JOIN [sys].[pdw_health_component_groups] AS g   
        ON c.[group_id] = g.[group_id]  
    INNER JOIN [sys].[pdw_health_alerts] AS a   
        ON aa.[alert_id] = a.[alert_id] and aa.[component_id] = c.[component_id]  
ORDER BY  
    a.alert_id ,  
    aa.[pdw_node_id];  
```  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->
[設備監視&#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
