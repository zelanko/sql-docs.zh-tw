---
title: 啟用 FileTable 的必要條件 | Microsoft Docs
description: 若要使用 Filetable，請先開啟 FILESTREAM、指定目錄，然後設定特定選項和存取層級。 了解如何符合所有必要條件。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], prerequisites
ms.assetid: 6286468c-9dc9-4eda-9961-071d2a36ebd6
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
ms.openlocfilehash: 12e392d083b9b47e3330d8a95b6c2d199a146cea
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809911"
---
# <a name="enable-the-prerequisites-for-filetable"></a>啟用 FileTable 的必要條件
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  描述如何啟用建立和使用 FileTable 的必要元件。  
  
##  <a name="enabling-the-prerequisites-for-filetable"></a><a name="EnablePrereq"></a> 啟用 FileTable 的必要條件  
 若要啟用建立和使用 FileTable 的必要條件，請啟用下列項目：  
  
-   **於執行個體層級：**  
  
    -   [在執行個體層級啟用 FILESTREAM](#BasicsFilestream)  
  
-   **於資料庫層級：**  
  
    -   [在資料庫層級提供 FILESTREAM 檔案群組](#filegroup)  
  
    -   [在資料庫層級啟用非交易式存取](#BasicsNTAccess)  
  
    -   [在資料庫層級指定 FileTable 的目錄](#BasicsDirectory)  
  
##  <a name="enabling-filestream-at-the-instance-level"></a><a name="BasicsFilestream"></a> 在執行個體層級啟用 FILESTREAM  
 FileTable 會擴充 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之 FILESTREAM 功能的能力。 因此，您必須先在 Windows 層級和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上啟用 FILESTREAM 的檔案 I/O 存取，然後才能建立和使用 FileTable。  
  
###  <a name="how-to-enable-filestream-at-the-instance-level"></a><a name="HowToFilestream"></a> 如何：在執行個體層級啟用 FILESTREAM  
 如需如何啟用 FILESTREAM 的相關資訊，請參閱 [啟用及設定 FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)。  
  
 當您呼叫 **sp_configure** 以在執行個體層級啟用 FILESTREAM 時，必須將 filestream_access_level 選項設定為 2。 如需詳細資訊，請參閱 [Filestream 存取層級伺服器組態選項](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md)。  
  
###  <a name="how-to-allow-filestream-through-the-firewall"></a><a name="firewall"></a> 如何：允許 FILESTREAM 通過防火牆  
 如需有關如何允許 FILESTREAM 通過防火牆的詳細資訊，請參閱＜ [Configure a Firewall for FILESTREAM Access](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)＞。  
  
##  <a name="providing-a-filestream-filegroup-at-the-database-level"></a><a name="filegroup"></a> 在資料庫層級提供 FILESTREAM 檔案群組  
 資料庫必須具有 FILESTREAM 檔案群組，然後您才能在該資料庫中建立 FileTable。 如需此必要條件的詳細資訊，請參閱 [建立啟用 FILESTREAM 的資料庫](../../relational-databases/blob/create-a-filestream-enabled-database.md)。  
  
##  <a name="enabling-non-transactional-access-at-the-database-level"></a><a name="BasicsNTAccess"></a> 在資料庫層級啟用非交易式存取  
 FileTable 可讓 Windows 應用程式取得 FILESTREAM 資料的 Windows 檔案控制代碼，而不需要使用交易。 若要允許對儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的檔案進行這種非交易式存取，您必須針對將包含 FileTable 的每個資料庫，指定在資料庫層級啟用非交易式存取的所需層級。  
  
###  <a name="how-to-check-whether-non-transactional-access-is-enabled-on-databases"></a><a name="HowToCheckAccess"></a> 如何：檢查是否已在資料庫上啟用非交易式存取  
 查詢 [sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md) 目錄檢視，並檢查 **non_transacted_access** 和 **non_transacted_access_desc** 資料行。  

```sql
SELECT DB_NAME(database_id), non_transacted_access, non_transacted_access_desc  
    FROM sys.database_filestream_options;  
GO  
```

###  <a name="how-to-enable-non-transactional-access-at-the-database-level"></a><a name="HowToNTAccess"></a> 如何：在資料庫層級啟用非交易式存取  
 非交易式存取的可用層級是 FULL、READ_ONLY 和 OFF。  
  
 **使用 Transact-SQL 指定非交易式存取的層級**  
 - **建立新資料庫**時，請使用 **NON_TRANSACTED_ACCESS** FILESTREAM 選項，呼叫 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md) 陳述式。

   ```sql
   CREATE DATABASE database_name  
     WITH FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' )  
   ```

- **改變現有資料庫**時，請使用 **NON_TRANSACTED_ACCESS** FILESTREAM 選項，呼叫 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md) 陳述式。

   ```sql
   ALTER DATABASE database_name  
     SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' )  
   ```

 **使用 SQL Server Management Studio 指定非交易式存取的層級**  
 在 [資料庫屬性]  對話方塊中，您可以透過 [選項]  頁面的 [FILESTREAM 非交易式存取]  欄位，來指定非交易式存取的層級。 如需此對話方塊的詳細資訊，請參閱[資料庫屬性 &#40;選項頁面&#41;](../../relational-databases/databases/database-properties-options-page.md)。  
  
##  <a name="specifying-a-directory-for-filetables-at-the-database-level"></a><a name="BasicsDirectory"></a> 在資料庫層級指定 FileTable 的目錄  
 當您在資料庫層級啟用檔案的非交易式存取時，可以選擇性地使用 **DIRECTORY_NAME** 選項，一併提供目錄名稱。 如果您在啟用非交易式存取時沒有提供目錄名稱，則之後必須先提供此名稱，然後才能在資料庫中建立 FileTable。  
  
 在 FileTable 資料夾階層中，這個資料庫層級目錄會成為在執行個體層級中針對 FILESTREAM 指定之共用名稱的子系，以及在資料庫中建立之 FileTable 的父系。 如需詳細資訊，請參閱 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)。  
  
###  <a name="how-to-specify-a-directory-for-filetables-at-the-database-level"></a><a name="HowToDirectory"></a> 如何：在資料庫層級指定 FileTable 的目錄  
 跨資料庫層級目錄的執行個體中，指定的名稱必須是唯一的。  
  
**使用 Transact-SQL 指定 FileTable 的目錄**  
- **建立新資料庫**時，請使用 **DIRECTORY_NAME** FILESTREAM 選項，呼叫 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md) 陳述式。

   ```sql
   CREATE DATABASE database_name  
     WITH FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' );  
   GO  
   ```

-   **改變現有資料庫**時，請使用 **DIRECTORY_NAME** FILESTREAM 選項，呼叫 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md) 陳述式。 當您使用這些選項來變更目錄名稱時，資料庫必須獨佔鎖定，而且沒有任何開啟的檔案控制代碼。  
  
    ```sql  
    ALTER DATABASE database_name  
        SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
-   **附加資料庫**時，請使用 **FOR ATTACH** 選項和 **DIRECTORY_NAME** FILESTREAM 選項，呼叫 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md) 陳述式。  
  
    ```sql  
    CREATE DATABASE database_name  
        FOR ATTACH WITH FILESTREAM ( DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
-   **還原資料庫**時，請使用 **DIRECTORY_NAME** FILESTREAM 選項，呼叫 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md) 陳述式。  
  
    ```sql  
    RESTORE DATABASE database_name  
        WITH FILESTREAM ( DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
 **使用 SQL Server Management Studio 指定 FileTable 的目錄**  
 在 [資料庫屬性]  對話方塊中，您可以透過 [選項]  頁面的 [FILESTREAM 目錄名稱]  欄位，來指定目錄名稱。 如需此對話方塊的詳細資訊，請參閱[資料庫屬性 &#40;選項頁面&#41;](../../relational-databases/databases/database-properties-options-page.md)。  
  
###  <a name="how-to-view-existing-directory-names-for-the-instance"></a><a name="viewnames"></a> 如何：檢視執行個體的現有目錄名稱  
 若要檢視執行個體的現有目錄名稱清單，請查詢 [sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md) 目錄檢視，並檢查 **filestream_database_directory_name** 資料行。  
  
```sql  
SELECT DB_NAME ( database_id ), directory_name  
    FROM sys.database_filestream_options;  
GO  
```  
  
###  <a name="requirements-and-restrictions-for-the-database-level-directory"></a><a name="ReqDirectory"></a> 資料庫層級目錄的需求和限制  
  
-   當您呼叫 **CREATE DATABASE** 或 **ALTER DATABASE** 時， **DIRECTORY_NAME**是選擇性設定。 如果您沒有指定 **DIRECTORY_NAME**的值，則目錄名稱會維持 Null。 不過，如果您未在資料庫層級中指定 **DIRECTORY_NAME** 的值，就無法在資料庫中建立 FileTable。  
  
-   您所提供的目錄名稱必須符合有效目錄名稱的檔案系統需求。  
  
-   當資料庫包含 FileTable 時，您無法將 **DIRECTORY_NAME** 設定回 Null 值。  
  
-   當您附加或還原資料庫時，如果新的資料庫具有已經存在目標執行個體中的 **DIRECTORY_NAME** 值，此作業就會失敗。 因此，當您呼叫 **CREATE DATABASE FOR ATTACH** 或 **RESTORE DATABASE** 時，請針對 **DIRECTORY_NAME**指定唯一的值。  
  
-   當您將現有的資料庫升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]時， **DIRECTORY_NAME** 的值為 Null。  
  
-   當您在資料庫層級中啟用或停用非交易式存取時，此作業不會檢查是否已經指定目錄名稱，或者目錄名稱是否唯一。  
  
-   當您卸除為 FileTable 啟用的資料庫時，會一併移除資料庫層級目錄和其下所有 FileTable 的全部目錄結構。  
  
