---
title: 查看已註冊封裝的擴充事件目標 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- targets [SQL Server extended events]
- viewing event targets
- extended events [SQL Server], viewing targets
ms.assetid: 4985aa5f-ac99-49f6-852c-9d25916549e9
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 8e796d141ef943399fc2469c232b34b1956cef3b
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84927303"
---
# <a name="view-the-extended-events-targets-for-registered-packages"></a>檢視已註冊之封裝的擴充事件目標
  在您建立 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 「擴充事件」工作階段之前，判斷哪些「擴充事件」目標可用會非常實用。 這項工作需要在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中使用查詢編輯器來執行以下程序。  
  
 當此程序中的陳述式完成之後，查詢編輯器的 **[結果]** 索引標籤會顯示以下兩個資料行：  
  
-   package_name  
  
-   target_name  
  
## <a name="to-view-the-extended-events-targets-for-registered-packages-using-query-editor"></a>若要使用查詢編輯器來檢視已註冊之封裝的擴充事件目標  
  
-   在查詢編輯器中，發出下列陳述式。  
  
    ```  
    USE msdb  
    SELECT p.name package_name, o.name target_name  
    FROM sys.dm_xe_objects o  
    JOIN sys.dm_xe_packages p  
         ON o.package_guid = p.guid  
    WHERE o.object_type = 'target'  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 擴充事件目標](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [dm_xe_objects &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
