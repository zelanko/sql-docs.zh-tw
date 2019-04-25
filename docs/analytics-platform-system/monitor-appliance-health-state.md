---
title: 監視設備健全狀況-Analytics Platform System
description: 如何使用管理主控台中，或直接查詢的平行處理資料倉儲動態管理檢視來監視 Analytics Platform System appliance 的狀態。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d8616d291dcaa8afadc01c9bd237903ca6c13573
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62640025"
---
# <a name="monitor-appliance-health-state"></a>監視設備健全狀況狀態
這篇文章說明如何使用管理主控台中，或直接查詢的平行處理資料倉儲動態管理檢視來監視 Analytics Platform System appliance 的狀態。 
  
## <a name="to-monitor-the-appliance-state"></a>若要監視的應用裝置狀態  
系統管理員可以使用系統管理員主控台] 或 [SQL Server PDW 動態管理檢視 (Dmv) 來擷取完整的階層架構的節點、 元件和軟體。 下圖提供高層級的了解 SQL Server PDW 監視的元件。  
  
![監視概觀](./media/monitor-appliance-health-state/SQL_Server_PDW_Monitoring_Overview.png "SQL_Server_PDW_Monitoring_Overview")  
  
### <a name="monitor-component-status-by-using-the-admin-console"></a>使用管理主控台的監視元件狀態  
若要使用管理主控台，以擷取元件狀態：  
  
1.  按一下 [**設備狀態**] 索引標籤。  
  
2.  在應用裝置狀態 頁面上，按一下特定的節點，以檢視節點詳細資料。  
  
    ![PDW 管理主控台狀態](./media/monitor-appliance-health-state/SQL_Server_PDW_AdminConsol_State.png "SQL_Server_PDW_AdminConsol_State")  
  
### <a name="monitor-component-status-by-using-system-views"></a>使用系統檢視表的監視元件狀態  
若要使用系統檢視表，以擷取元件狀態，請使用[sys.dm_pdw_component_health_status](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)。 例如，下列查詢會擷取所有元件的狀態。  
  
```sql  
SELECT   
   s.[pdw_node_id],  
   n.[name] as [node_name],  
   n.[address] ,  
   g.[group_id] ,  
   g.[group_name] ,  
   c.[component_id] ,  
   c.[component_name] ,  
   s.[component_instance_id] ,   
   p.[property_name] ,  
   s.[property_value] ,  
   s.[update_time]  
FROM [sys].[dm_pdw_component_health_status] AS s  
JOIN sys.dm_pdw_nodes AS n   
   ON s.[pdw_node_id] = n.[pdw_node_id]  
JOIN [sys].[pdw_health_components] AS c   
   ON s.[component_id] = c.[component_id]  
JOIN [sys].[pdw_health_component_groups] AS g   
   ON c.[group_id] = g.[group_id]  
JOIN [sys].[pdw_health_component_properties] AS p   
   ON s.[property_id] = p.[property_id] AND s.[component_id] = p.[component_id]  
WHERE p.property_name = 'Status'  
ORDER BY  
   s.[pdw_node_id],  
   g.[group_name] ,   
   s.[component_instance_id] ,  
   c.[component_name] ,   
   p.[property_name];  
```  
  
針對 [狀態] 屬性所傳回的可能值如下：  
  
-   確定  
  
-   NonCritical  
  
-   嚴重  
  
-   Unknown  
  
-   不支援  
  
-   無法連線  
  
-   無法復原  
  
若要查看所有元件的所有屬性，請移除`WHERE  p.property_name = 'Status'`子句。  
  
**[Update_time]** 欄會顯示最後一次輪詢 SQL Server PDW 健康情況代理程式元件。  
  
> [!CAUTION]  
> 請務必調查問題時有不被輪詢元件，5 分鐘或更久，可能表示有問題軟體的活動訊號警示。  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[設備監視&#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
