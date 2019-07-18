---
title: Master 資料庫-Parallel Data Warehouse |Microsoft Docs
description: 深入了解平行處理資料倉儲中的 master 資料庫。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 9f37c7a85baea3b41f6016a57e4f57579b427719
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960657"
---
# <a name="master-database---parallel-data-warehouse"></a>Master 資料庫-平行處理資料倉儲
SQL Server PDW master 資料庫儲存應用裝置層級登入資訊和資料庫目錄。 它是位於 [控制] 節點的 SQL Server master 資料庫。 因此，提供類似的功能與 SQL Server PDW 主要提供給 SQL Server。  
  
如需有關系統資料庫的詳細資訊，請參閱[系統資料庫](system-databases.md)。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
下列清單描述您無法在 SQL Server PDW master 資料庫執行的作業。  
  
您*無法：*  
  
-   執行主要的差異備份。  
  
-   在 master 中建立使用者物件。  
  
-   變更主機的定序。  
  
-   變更主要擁有者。  
  
-   卸除或重新命名主要。  
  
-   修改主機的權限。  
  
-   執行**DBCC SHRINKLOG**。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作|描述|  
|--------|---------------|  
|建立主要的完整備份。|範例<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />如需詳細資訊，請參閱 < [BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)。|  
|還原 master 資料庫|若要還原 master 資料庫，請使用[還原 Master 資料庫](restore-the-master-database.md)組態管理員工具中的頁面。|  
|檢視資料庫目錄資訊。|`SELECT * FROM master.sys.databases;`|  
|檢視全系統的登入和權限資訊。|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
