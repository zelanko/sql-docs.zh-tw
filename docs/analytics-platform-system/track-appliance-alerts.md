---
title: 追蹤設備警示
description: 追蹤分析平臺系統中的設備警示。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 03568666367bf6273f197994f572bbbbd62bb42e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74399946"
---
# <a name="track-appliance-alerts-in-analytics-platform-system"></a>在分析平臺系統中追蹤設備警示
本主題說明如何使用管理主控台和系統檢視來追蹤 SQL Server PDW 應用裝置中的警示。  
  
## <a name="to-track-appliance-alerts"></a>追蹤設備警示  
SQL Server PDW 會針對需要注意的硬體和軟體問題建立警示。 每個警示都包含問題的標題和描述。  
  
SQL Server PDW 會記錄[sys.databases dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md) DMV 中的警示。 系統會保留10000警示的限制，並在超過限制時先刪除最舊的警示。  
  
### <a name="view-alerts-by-using-the-admin-console"></a>使用管理主控台來查看警示  
適用于 PDW 區域的 [**警示**] 索引標籤，以及設備的網狀架構區域。 發生容錯移轉之後，容錯移轉事件就會包含在頁面上的警示數目中。 [PDW] 區域和設備的 [網狀架構] 區域都有一個頁面。 每個健全狀況頁面都有一個索引標籤。若要深入瞭解警示，請按一下 [**健康**情況] 頁面、[**警示**] 索引標籤，然後按一下警示。  
  
![PDW 管理主控台警示](./media/track-appliance-alerts/SQL_Server_PDW_AdminConsole_AlertsV2.png "SQL_Server_PDW_AdminConsole_AlertsV2")  
  
在 [**警示**] 頁面上：  
  
-   若要查看警示歷程記錄，請按一下 [**審查警示歷程記錄**] 連結。  
  
-   若要查看警示元件及其目前的屬性值，請按一下 [警示] 資料列。  
  
-   若要查看引發警示之節點的詳細資料，請按一下節點名稱。  
  
### <a name="view-alerts-by-using-the-system-views"></a>使用系統檢視來查看警示  
若要使用系統檢視來查看警示，請查詢[sys. dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)。 此 DMV 會顯示尚未更正的警示。 如需有關分類警示和錯誤的說明，請使用[sys.databases dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md) DMV。  
  
下列範例是用來查看目前警示的常見查詢。  
  
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
[&#40;分析平臺系統&#41;的設備監視](appliance-monitoring.md)  
  
