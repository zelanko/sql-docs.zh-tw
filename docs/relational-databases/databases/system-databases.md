---
title: 系統資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- system databases [SQL Server]
- displaying system database data
- modifying system data
- viewing system database data
ms.assetid: 30468a7c-4225-4d35-aa4a-ffa7da4f1282
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d5bf6819d26ff105113292162c3302d54460a6e1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="system-databases"></a>系統資料庫
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包括下列系統資料庫。  
  
|系統資料庫|描述|  
|---------------------|-----------------|  
|[master 資料庫](../../relational-databases/databases/master-database.md)|記錄 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的所有系統層級資訊。|  
|[msdb 資料庫](../../relational-databases/databases/msdb-database.md)|由 SQL Server Agent 用於排程警示和作業。|  
|[Model 資料庫](../../relational-databases/databases/model-database.md)|用來當作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上建立之所有資料庫的範本。 對 **model** 資料庫進行的修改 (例如，資料庫大小、定序、復原模式和其他資料庫選項) 會套用到之後建立的任何資料庫。|  
|[Resource 資料庫](../../relational-databases/databases/resource-database.md)|是一個唯讀的資料庫，其中包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]擁有的系統物件。 系統物件實際上會保存在 **Resource** 資料庫中，但邏輯上會出現在每個資料庫的 **sys** 結構描述中。|  
|[tempdb 資料庫](../../relational-databases/databases/tempdb-database.md)|是保存暫存物件或中繼結果集的工作空間。|  

> [!IMPORTANT]
> 針對 Azure SQL Database，只會套用 master 資料庫和 tempdb 資料庫。 如需邏輯伺服器和邏輯 master 資料庫的概念，請參閱[什麼是 Azure SQL 邏輯伺服器？](https://docs.microsoft.com/azure/sql-database/sql-database-servers-databases#what-is-an-azure-sql-logical-server)。 如需 Azure SQL Database 內容中 tempdb 的討論，請參閱 [Azure SQL Database 中的 tempdb 資料庫](tempdb-database.md#tempdb-database-in-sql-database)。
  
## <a name="modifying-system-data"></a>修改系統資料  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援使用者直接更新系統物件中的資訊，例如系統資料表、系統預存程序和目錄檢視。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 另外提供了一組完整的管理工具，讓使用者可以完全管理他們的系統，並管理資料庫中所有的使用者與物件。 這些選項包括：  
  
-   管理公用程式，例如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
-   SQL-SMO API。 可讓程式設計人員加入完整的功能，以在應用程式中管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼和預存程序。 上述項目可以使用系統預存程序和 [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 陳述式。  
  
 這些工具可避免應用程式在系統物件中被變更。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 有時需要在新版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中變更系統資料表，以支援加入該版本的新功能。 提出直接參考系統資料表的 SELECT 陳述式之應用程式，它們通常依賴系統資料表的舊有格式。 站台可能要等到重寫從系統資料表選取的應用程式之後，才能夠升級到新版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會考量系統預存程序、DDL 和 SQL-SMO 發行的介面，並努力維護這些介面的回溯相容性。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並不支援在系統資料表上定義的觸發程序，因為這些觸發程序可能會修改系統的作業。  
  
> [!NOTE]  
>  系統資料庫無法位於 UNC 共用目錄。  
  
## <a name="viewing-system-database-data"></a>檢視系統資料庫資料  
 您不應撰寫直接查詢系統資料表的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，除非這是取得應用程式所需資訊的唯一方式。 相反地，應用程式應使用下列方法取得目錄和系統資訊：  
  
-   系統目錄檢視  
  
-   SQL-SMO  
  
-   Windows Management Instrumentation (WMI) 介面  
  
-   用於應用程式的資料 API 之 Catalog 函數、方法、屬性 (attribute) 或屬性 (property)，例如 ADO、OLE DB 或 ODBC。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 系統預存程序和內建函數。  
  
## <a name="related-tasks"></a>相關工作  
 [系統資料庫的備份與還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [在物件總管中隱藏系統物件](http://msdn.microsoft.com/library/c01d8804-838c-4f75-b78c-80e41e4fffdc)  
  
## <a name="related-content"></a>相關內容  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
 [資料庫](../../relational-databases/databases/databases.md)  
  
  
