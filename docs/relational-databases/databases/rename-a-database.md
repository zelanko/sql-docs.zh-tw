---
title: 重新命名資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], renaming
- renaming databases
ms.assetid: 44c69d35-abcb-4da3-9370-5e0bc9a28496
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a0ea80a51a578f99cdff6189acacfe991ab34c43
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/12/2018
ms.locfileid: "51557835"
---
# <a name="rename-a-database"></a>重新命名資料庫

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 Azure SQL Database 中重新命名使用者定義的資料庫。 資料庫的名稱可以包含任何依照識別碼規則的字元。  
  
## <a name="in-this-topic"></a>本主題內容
  
- 開始之前：  
  
     [限制事項](#limitations-and-restrictions)  
  
     [Security](#security)  
  
- 使用下列方法重新命名資料庫：  
  
     [SQL Server Management Studio](#rename-a-database-using-sql-server-management-studio)  
  
     [Transact-SQL](#rename-a-database-using-transact-sql)  
  
- **Follow Up:**  [After renaming a database](#FollowUp)  

> [!NOTE]
> 若要重新命名 Azure SQL 資料倉儲或平行處理資料倉儲中的資料庫，請使用 [RENAME (Transact-SQL)](../../t-sql/statements/rename-transact-sql.md) 陳述式。
  
## <a name="before-you-begin"></a>開始之前
  
### <a name="limitations-and-restrictions"></a>限制事項  
  
- 您無法重新命名系統資料庫。
- 其他使用者正在存取資料庫時，無法變更資料庫名稱。 
  - 在 SQL Server 中，您可以設定單一使用者模式的資料庫，以關閉任何開啟的連線。 如需詳細資訊，請參閱[將資料庫設定為單一使用者模式](../../relational-databases/databases/set-a-database-to-single-user-mode.md)。
  - 在 Azure SQL Database 中，您必須確定沒有任何其他使用者有要重新命名之資料庫的開啟連線。
  
### <a name="security"></a>Security  
  
#### <a name="permissions"></a>[權限]

需要資料庫的 ALTER 權限。  
  
## <a name="rename-a-database-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 重新命名資料庫

使用 SQL Server Management Studio，透過下列步驟重新命名 SQL Server 或 Azure SQL 資料庫。
  
1. 在 [物件總管] 中，連線至 SQL 執行個體。  
  
2. 請確定資料庫沒有任何開啟的連線。 如果您使用 SQL Server，則可以[將資料庫設定為單一使用者模式](../../relational-databases/databases/set-a-database-to-single-user-mode.md)關閉任何開啟的連線，並防止其他使用者在您變更資料庫名稱時連線。  
  
3. 在 [物件總管] 中，展開 [資料庫]，並以滑鼠右鍵按一下要重新命名的資料庫，然後按一下 [重新命名]。  
  
4. 輸入新的資料庫名稱，然後按一下 **[確定]**。  
  
## <a name="rename-a-database-using-transact-sql"></a>使用 Transact-SQL 重新命名資料庫  
  
### <a name="to-rename-a-sql-server-database-by-placing-it-in-single-user-mode"></a>讓 SQL Server 資料庫進入單一使用者模式以重新予以命名

在 SQL Server Management Studio 中使用 T-SQL，透過下列步驟重新命名 SQL Server 資料庫，包括讓資料庫進入單一使用者模式的步驟，以及在重新命名之後，讓資料庫重新進入多使用者模式的步驟。
  
1. 連線至您執行個體的 `master` 資料庫。  
2. 開啟查詢視窗。  
3. 複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 這個範例會將 `MyTestDatabase` 資料庫的名稱變更為 `MyTestDatabaseCopy`。
  
   ```sql
   USE master;  
   GO  
   ALTER DATABASE MyTestDatabase SET SINGLE_USER WITH ROLLBACK IMMEDIATE
   GO
   ALTER DATABASE MyTestDatabase MODIFY NAME = MyTestDatabaseCopy ;
   GO  
   ALTER DATABASE MyTestDatabaseCopy SET MULTI_USER
   GO
   ```  

### <a name="to-rename-an-azure-sql-database-database"></a>重新命名 Azure SQL Database 資料庫

在 SQL Server Management Studio 中使用 T-SQL，透過下列步驟重新命名 Azure SQL 資料庫。
  
1. 連線至您執行個體的 `master` 資料庫。  
2. 開啟查詢視窗。
3. 請確定沒有人正在使用資料庫。
4. 複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 這個範例會將 `MyTestDatabase` 資料庫的名稱變更為 `MyTestDatabaseCopy`。
  
   ```sql
   ALTER DATABASE MyTestDatabase MODIFY NAME = MyTestDatabaseCopy ;
   ```  

## <a name="backup-after-renaming-a-database"></a>在重新命名資料庫之後備份  

在 SQL Server 中重新命名資料庫之後，請備份 `master` 資料庫。 在 Azure SQL Database 中，不需要這麼做，因為會自動備份。  
  
## <a name="see-also"></a>另請參閱

- [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)
- [資料庫識別碼](../../relational-databases/databases/database-identifiers.md)  