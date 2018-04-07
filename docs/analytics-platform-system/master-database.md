---
title: master 資料庫 (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c71617c0-6689-4f52-81c6-58f4cf7c7377
caps.latest.revision: 8
ms.workload: not set
ms.openlocfilehash: 0031e4720c7fbcf7e60b7e35a59d16ad31a24103
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="master-database"></a>master 資料庫
SQL Server PDW master 資料庫儲存應用裝置層級登入資訊和資料庫目錄。 它是位於 [控制] 節點上的 SQL Server master 資料庫。 因此，它提供類似的功能與 SQL Server PDW 因為主要提供給 SQL Server。  
  
如需系統資料庫的詳細資訊，請參閱[系統資料庫](system-databases.md)。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
下列清單描述您無法在 SQL Server PDW master 資料庫執行的作業。  
  
您*無法：*  
  
-   執行主要的差異備份。  
  
-   在 master 中建立使用者物件。  
  
-   變更主要的定序。  
  
-   變更主要擁有者。  
  
-   卸除或重新命名主要。  
  
-   修改主機的權限。  
  
-   執行**DBCC SHRINKLOG**。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作|Description|  
|--------|---------------|  
|建立主要的完整備份。|範例：<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />如需詳細資訊，請參閱[BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)。|  
|還原 master 資料庫|若要還原 master 資料庫，請使用[還原 Master 資料庫](restore-the-master-database.md)組態管理員工具中的頁面。|  
|檢視資料庫的類別目錄資訊。|`SELECT * FROM master.sys.databases;`|  
|檢視全系統登入和權限資訊。|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
