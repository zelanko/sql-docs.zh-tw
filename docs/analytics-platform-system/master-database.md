---
title: Master 資料庫
description: 深入瞭解平行處理資料倉儲中的 master 資料庫。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 7bf3928bfb21d34d0f60e6c52be8dae43621e4bd
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766737"
---
# <a name="master-database---parallel-data-warehouse"></a>Master 資料庫-平行處理資料倉儲
SQL Server PDW master 資料庫會儲存設備層級的登入資訊和資料庫目錄。 它是位於控制節點上的 SQL Server master 資料庫。 因此，它提供了類似的功能，可 SQL Server PDW 作為主要提供給 SQL Server。  
  
如需系統資料庫的詳細資訊，請參閱 [系統資料庫](system-databases.md)。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
下列清單描述您無法在 SQL Server PDW master 資料庫上執行的作業。  
  
您 *無法：*  
  
-   執行 master 的差異備份。  
  
-   在 master 中建立使用者物件。  
  
-   變更 master 的定序。  
  
-   變更 master 的擁有者。  
  
-   卸載或重新命名 master。  
  
-   修改 master 的許可權。  
  
-   執行 **DBCC SHRINKLOG**。  
  
## <a name="related-tasks"></a>相關工作  
  
|Task|描述|  
|--------|---------------|  
|建立 master 的完整備份。|範例：<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />如需詳細資訊，請參閱 [備份資料庫](../t-sql/statements/backup-transact-sql.md?view=aps-pdw-2016)。|  
|還原 master 資料庫|若要還原 master 資料庫，請使用 Configuration Manager 工具中的 [ [還原 Master 資料庫](restore-the-master-database.md) ] 頁面。|  
|查看資料庫目錄資訊。|`SELECT * FROM master.sys.databases;`|  
|查看全系統登入和許可權資訊。|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
