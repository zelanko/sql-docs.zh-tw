---
title: 系統資料表 (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server]
- tables [SQL Server], system tables
- information retrieval [SQL Server]
- status information [SQL Server], system tables
- system information [SQL Server]
- system tables [SQL Server]
- system tables [SQL Server], about system tables
- system tables [SQL Server], retrieving information from
- retrieving system table information
ms.assetid: 56b8ad51-930c-4e5c-8d99-8c939d5b70ac
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2658b6ab0687a3eb3c63d6d658f93ff2c25b55c6
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38047213"
---
# <a name="system-tables-transact-sql"></a>系統資料表 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本章節的主題介紹 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的系統資料表。  
  
 任何使用者都不應直接變更系統資料表。 例如，請勿嘗試利用 DELETE、UPDATE 或 INSERT 陳述式，或使用者自訂觸發程序來修改系統資料表。  
  
 您可以參考系統資料表中的記載資料行。 不過，系統資料表中的許多資料行都沒有記載。 應用程式不應撰寫成直接查詢未記載的資料行。 相反地，若要擷取系統資料表所儲存的資訊，應用程式應該使用下列任何元件之一：  
  
-   系統預存程序  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式和函數  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件 (SMO)  
  
-   Replication Management Objects (RMO)  
  
-   資料庫 API 目錄函數  
  
 這些元件組成已發行的 API，以用來取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的系統資訊。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 會維護這些元件在各版本之間的相容性。 系統資料表的格式視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的內部架構而定，各版本之間可能不相同。 因此，直接存取系統資料表未記載之資料行的應用程式，可能需要改變，然後才能存取較新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。  
  
## <a name="in-this-section"></a>本節內容  
 系統資料表主題依下列功能區來組織：  
  
|||  
|-|-|  
|[備份與還原資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)|[記錄傳送資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-tables-transact-sql.md)|  
|[變更資料擷取資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/change-data-capture-tables-transact-sql.md)|[複寫資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)|  
|[資料庫維護計畫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/database-maintenance-plan-tables-transact-sql.md)|[SQL Server Agent 資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)|  
|[SQL Server 擴充事件目錄資料表&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/6d52ff03-f5aa-4f0f-8c98-9b49dc76f94e)|[sys.sysoledbusers &#40;Transact SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysoledbusers-transact-sql.md)|  
|[Integration Services 資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/integration-services-tables-transact-sql.md)|[systranschemas &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)|  
  
## <a name="see-also"></a>另請參閱  
 [相容性檢視&#40;Transact SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
