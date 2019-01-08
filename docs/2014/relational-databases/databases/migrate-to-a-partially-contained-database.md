---
title: 移轉至部分自主資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- contained database, migrating to
ms.assetid: 90faac38-f79e-496d-b589-e8b2fe01c562
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e8a7910b943b3d913e419d49fa4641bdc689e4e0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52803690"
---
# <a name="migrate-to-a-partially-contained-database"></a>Migrate to a Partially Contained Database
  此主題討論如何準備變更為部分自主資料庫模型，然後提供移轉步驟。  
  
 **本主題內容：**  
  
-   [準備移轉資料庫](#prepare)  
  
-   [啟用自主資料庫](#enable)  
  
-   [將資料庫轉換成部分自主資料庫](#convert)  
  
-   [將使用者移轉至自主資料庫使用者](#users)  
  
##  <a name="prepare"></a> 準備移轉資料庫  
 當您考慮將資料庫移轉至部分自主資料庫模型時，請檢閱下列項目。  
  
-   您應該了解部分自主資料庫模型。 如需詳細資訊，請參閱 [自主資料庫](contained-databases.md)。  
  
-   您應該了解部分自主資料庫獨有的風險。 如需詳細資訊，請參閱 [Security Best Practices with Contained Databases](security-best-practices-with-contained-databases.md)。  
  
-   自主資料庫不支援複寫、異動資料擷取，或變更追蹤。 請確認資料庫不會使用這些功能。  
  
-   請檢閱針對部分自主資料庫修改的資料庫功能清單。 如需詳細資訊，請參閱[修改的功能 &#40;自主資料庫&#41;](modified-features-contained-database.md)。  
  
-   請查詢 [sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql) 來尋找資料庫中的非內含性物件或功能。 如需詳細資訊，請參閱。  
  
-   請監視 **database_uncontained_usage** XEvent 來查看使用非內含性功能的時間。  
  
##  <a name="enable"></a> 啟用自主資料庫  
 您必須先在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體上啟用自主資料庫，然後才能建立自主資料庫。  
  
### <a name="enabling-contained-databases-using-transact-sql"></a>使用 Transact-SQL 來啟用自主資料庫  
 下列範例會在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體上啟用自主資料庫。  
  
```tsql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE ;  
GO  
```  
  
#### <a name="enabling-contained-databases-using-management-studio"></a>使用 Management Studio 來啟用自主資料庫  
 下列範例會在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體上啟用自主資料庫。  
  
1.  在物件總管中，以滑鼠右鍵按一下伺服器名稱，然後按一下 [屬性]。  
  
2.  在 [進階] 頁面的 [內含項目] 區段中，將 [啟用自主資料庫] 選項設定為 [True]。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="convert"></a> 將資料庫轉換成部分自主資料庫  
 您可以透過變更 [內含項目] 選項，將資料庫轉換成自主資料庫。  
  
### <a name="converting-a-database-to-partially-contained-using-transact-sql"></a>使用 Transact-SQL，將資料庫轉換成部分自主資料庫  
 下列範例會將名為 `Accounting` 的資料庫轉換成部分自主資料庫。  
  
```tsql  
USE [master]  
GO  
ALTER DATABASE [Accounting] SET CONTAINMENT = PARTIAL  
GO  
```  
  
### <a name="converting-a-database-to-partially-contained-using-management-studio"></a>使用 Management Studio，將資料庫轉換成部分自主資料庫  
 下列範例會將資料庫轉換成部分自主資料庫。  
  
1.  在物件總管中，展開 [資料庫]，以滑鼠右鍵按一下要轉換的資料庫，然後按一下 [屬性]。  
  
2.  在 [選項] 頁面上，將 [內含項目類型] 選項變更為 [部分]。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="users"></a> 將使用者移轉至自主資料庫使用者  
 下列範例會將以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入為基礎的所有使用者移轉至具有密碼之自主資料庫使用者。 此範例會排除未啟用的登入。 您必須在自主資料庫中執行此範例。  
  
```tsql  
DECLARE @username sysname ;  
DECLARE user_cursor CURSOR  
    FOR   
        SELECT dp.name   
        FROM sys.database_principals AS dp  
        JOIN sys.server_principals AS sp   
        ON dp.sid = sp.sid  
        WHERE dp.authentication_type = 1 AND sp.is_disabled = 0;  
OPEN user_cursor  
FETCH NEXT FROM user_cursor INTO @username  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        EXECUTE sp_migrate_user_to_contained   
        @username = @username,  
        @rename = N'keep_name',  
        @disablelogin = N'disable_login';  
    FETCH NEXT FROM user_cursor INTO @username  
    END  
CLOSE user_cursor ;  
DEALLOCATE user_cursor ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [自主資料庫](contained-databases.md)   
 [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql)   
 [sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql)  
  
  
