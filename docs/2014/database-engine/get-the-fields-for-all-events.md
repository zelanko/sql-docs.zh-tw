---
title: 取得所有事件的欄位 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], getting fields
- xe
ms.assetid: 4e4ee03f-5bca-42ed-a37c-db1c82e3aad2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0838367ad699c1278bb6ec42f28161ba76c6fd5
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66064793"
---
# <a name="get-the-fields-for-all-events"></a>取得所有事件的欄位
  完成此工作涉及在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中使用查詢編輯器。  
  
 當此程序中的陳述式完成之後，查詢編輯器的 **[結果]** 索引標籤會顯示以下資料行：  
  
-   package_name  
  
-   event_name  
  
-   event_field  
  
-   field_type  
  
-   column_type  
  
 當您設定使用值區目標的事件工作階段時，可以使用上述的資訊。 如需詳細資訊，請參閱＜ [SQL Server Extended Events Targets](../../2014/database-engine/sql-server-extended-events-targets.md)＞。  
  
## <a name="before-you-begin"></a>開始之前  
 在您建立 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 擴充事件工作階段之前，取得與事件相關之欄位的資訊會非常有用。  
  
## <a name="to-get-the-fields-for-all-events-using-query-editor"></a>若要使用查詢編輯器取得所有事件的欄位  
  
-   在查詢編輯器中，發出下列陳述式。  
  
    ```  
    select p.name package_name, o.name event_name, c.name event_field, c.type_name field_type, c.column_type column_type  
    from sys.dm_xe_objects o  
    join sys.dm_xe_packages p  
          on o.package_guid = p.guid  
    join sys.dm_xe_object_columns c  
          on o.name = c.object_name  
    where o.object_type = 'event'  
    order by package_name, event_name  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_xe_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
