---
title: 檢視已註冊之封裝的事件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- viewing events
- extended events [SQL Server], viewing events
ms.assetid: 9a90b1a2-aa69-43f6-bdeb-cc5f57a26c6f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1156a7272edc8ad1ecfb8e173f81bc678800c855
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66089625"
---
# <a name="view-the-events-for-registered-packages"></a>檢視已註冊之封裝的事件
  在您建立 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 擴充的事件工作階段之前，找出註冊之封裝中可用的事件會非常有用。 如需詳細資訊，請參閱＜ [SQL Server Extended Events Packages](../relational-databases/extended-events/sql-server-extended-events-packages.md)＞。  
  
 完成這項工作需要在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中使用查詢編輯器來進行以下程序。  
  
 當此程序中的陳述式完成之後，查詢編輯器的 **[結果]** 索引標籤會顯示以下資料行：  
  
-   名稱。 封裝名稱。  
  
-   事件。 事件名稱。  
  
-   關鍵字。 衍生自內部數值對應資料表的關鍵字。  
  
-   通道。 事件的使用者。  
  
-   描述。 事件描述。  
  
## <a name="to-view-the-events-for-registered-packages-using-query-editor"></a>若要使用查詢編輯器來檢視已註冊之封裝的事件  
  
-   在查詢編輯器中，發出下列陳述式。  
  
    ```  
    USE msdb  
    SELECT p.name, c.event, k.keyword, c.channel, c.description FROM  
    (  
    SELECT event_package=o.package_guid, o.description,   
    event=c.object_name, channel=v.map_value  
    FROM sys.dm_xe_objects o  
    LEFT JOIN sys.dm_xe_object_columns c ON o.name=c.object_name  
    INNER JOIN sys.dm_xe_map_values v ON c.type_name=v.name   
    AND c.column_value=cast(v.map_key AS nvarchar)  
    WHERE object_type='event' AND (c.name='CHANNEL' or c.name IS NULL)  
  
    ) c LEFT JOIN   
    (  
    SELECT event_package=c.object_package_guid, event=c.object_name,   
    keyword=v.map_value  
    FROM sys.dm_xe_object_columns c INNER JOIN sys.dm_xe_map_values v   
    ON c.type_name=v.name AND c.column_value=v.map_key   
    AND c.type_package_guid=v.object_package_guid  
    INNER JOIN sys.dm_xe_objects o ON o.name=c.object_name   
    AND o.package_guid=c.object_package_guid  
    WHERE object_type='event' AND c.name='KEYWORD'   
    ) k  
    ON  
    k.event_package=c.event_package AND (k.event=c.event or k.event IS NULL)  
    INNER JOIN sys.dm_xe_packages p ON p.guid=c.event_package  
    ORDER BY keyword desc, channel, event  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 擴充事件封裝](../relational-databases/extended-events/sql-server-extended-events-packages.md)   
 [sys.dm_xe_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
