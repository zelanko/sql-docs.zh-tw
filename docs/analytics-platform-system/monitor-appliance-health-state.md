---
title: 監視設備健全狀況
description: 如何使用管理主控台或直接查詢平行處理資料倉儲動態管理檢視，來監視分析平臺系統裝置的狀態。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b99123f81fcdddd74dc72d485d97e428ca59ed84
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400997"
---
# <a name="monitor-appliance-health-state"></a>監視設備健全狀況狀態
本文說明如何使用管理主控台或直接查詢平行處理資料倉儲動態管理檢視，來監視 Analytics Platform System 設備的狀態。 
  
## <a name="to-monitor-the-appliance-state"></a>監視設備狀態  
系統管理員可以使用管理主控台或 SQL Server PDW 動態管理檢視（Dmv）來取得節點、元件和軟體的完整階層。 下圖對 SQL Server PDW 監視的元件提供高階的瞭解。  
  
![監視概觀](./media/monitor-appliance-health-state/SQL_Server_PDW_Monitoring_Overview.png "SQL_Server_PDW_Monitoring_Overview")  
  
### <a name="monitor-component-status-by-using-the-admin-console"></a>使用管理主控台監視元件狀態  
若要使用管理主控台抓取元件狀態：  
  
1.  按一下 [**設備狀態**] 索引標籤。  
  
2.  在 [設備狀態] 頁面上，按一下特定節點以查看節點詳細資料。  
  
    ![PDW 管理主控台狀態](./media/monitor-appliance-health-state/SQL_Server_PDW_AdminConsol_State.png "SQL_Server_PDW_AdminConsol_State")  
  
### <a name="monitor-component-status-by-using-system-views"></a>使用系統檢視來監視元件狀態  
若要使用系統檢視來取出元件狀態，請使用[sys.databases。 dm_pdw_component_health_status](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)。 例如，下列查詢會抓取所有元件的狀態。  
  
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
  
Status 屬性傳回的可能值為：  
  
-   確定  
  
-   非  
  
-   重大  
  
-   Unknown  
  
-   不支援  
  
-   無法連線  
  
-   無法復原  
  
若要查看所有元件的所有屬性，請移除`WHERE  p.property_name = 'Status'`子句。  
  
**[Update_time]** 資料行會顯示 SQL Server PDW 健康情況代理程式上次輪詢元件的時間。  
  
> [!CAUTION]  
> 當元件未輪詢5分鐘或更久時，請務必調查問題;可能會有警示指出軟體信號的問題。  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[&#40;分析平臺系統&#41;的設備監視](appliance-monitoring.md)  
  
