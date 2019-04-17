---
title: 為複寫啟用資料庫 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server replication]
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ac332e77226d5de33a4ef7fc77a0c34f6b234a3b
ms.sourcegitcommit: b2a29f9659f627116d0a92c03529aafc60e1b85a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/12/2019
ms.locfileid: "59516484"
---
# <a name="enable-a-database-for-replication-sql-server-management-studio"></a>為複寫啟用資料庫 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
**sysadmin** 固定伺服器角色成員使用「新增發行集精靈」建立發行集時，會為複寫隱含啟用資料庫。 **sysadmin** 固定伺服器角色成員同樣可以為複寫明確啟用資料庫，以便 **db_owner** 固定資料庫角色成員可以在該資料庫中建立一個或多個發行集。 若要明確啟用資料庫，請使用 [發行者屬性 - \<發行者>] 對話方塊的 [發行集資料庫] 頁面。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)＞。  
  
## <a name="using-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS)
  
1.  在 [發行者屬性 - \<發行者>] 對話方塊的 [發行集資料庫] 頁面中，針對您想要複寫的每個資料庫，選取 [異動] 及/或 [合併] 核取方塊。 選取 **[交易式]** 以為快照式複寫啟用資料庫。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
## <a name="using-transact-sql-t-sql"></a>使用 Transact-SQL (T-SQL)
您可以使用下列 Transact-SQL 程式碼來啟用用於複寫的資料庫： 

```sql
USE master
EXEC sp_replicationdboption @dbname = 'AdventureWorks2017',
@optname = 'publish',
@value = 'true'
GO
```

若要停用發行，請設定 @value = 'false'。 
