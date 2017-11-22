---
title: "使用資源管理員進行備份壓縮，以限制 CPU 使用率 (Transact-SQL) | Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backup compression [SQL Server], Resource Governor
- backup compression [SQL Server], CPU usage
- compression [SQL Server], backup compression
- backups [SQL Server], compression
- Resource Governor, backup compression
ms.assetid: 01796551-578d-4425-9b9e-d87210f7ba72
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 967060be06fd9b7769705aa0995ba288f9ba19f8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql"></a>使用資源管理員進行備份壓縮，以限制 CPU 使用率 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  根據預設，使用壓縮來備份會大幅增加 CPU 使用量，而且壓縮程序所耗用的額外 CPU 可能會對並行作業造成不良的影響。 因此，如果發生 CPU 爭用的情況，您可能會想要在[資源管理員](../../relational-databases/resource-governor/resource-governor.md) 限制 CPU 使用量的工作階段中，建立低優先權的壓縮備份。 這個主題所展示的狀況會將特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者的工作階段對應至在這類情況中限制 CPU 使用量的資源管理員工作負載群組，藉以分類這些工作階段。  
  
> [!IMPORTANT]  
>  在給定的資源管理員狀況中，工作階段分類可能會以使用者名稱、應用程式名稱，或可區分連接的其他任何項目為基礎。 如需相關資訊，請參閱 [Resource Governor Classifier Function](../../relational-databases/resource-governor/resource-governor-classifier-function.md) 以及 [Resource Governor Workload Group](../../relational-databases/resource-governor/resource-governor-workload-group.md)。  
  
##  <a name="Top"></a> 這個主題包含下列狀況集，並依序展示：  
  
1.  [針對低優先權作業設定登入和使用者](#setup_login_and_user)  
  
2.  [設定資源管理員來限制 CPU 使用量](#configure_RG)  
  
3.  [確認目前工作階段的分類 (Transact-SQL)](#verifying)  
  
4.  [使用含有限制 CPU 的工作階段來壓縮備份](#creating_compressed_backup)  
  
##  <a name="setup_login_and_user"></a> 針對低優先權作業設定登入和使用者  
 這個主題中的狀況需要使用低優先權 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和使用者。 使用者名稱將用來分類在登入中執行的工作階段，並且將它們路由傳送至限制 CPU 使用量的資源管理員工作負載群組。  
  
 下列程序描述的是針對此目的設定登入和使用者的步驟，後面接著 [!INCLUDE[tsql](../../includes/tsql-md.md)] 範例：「範例 A：設定登入和使用者 (Transact-SQL)」。  
  
### <a name="to-set-up-a-login-and-database-user-for-classifying-sessions"></a>設定登入和資料庫使用者以便分類工作階段  
  
1.  針對建立低優先權壓縮備份，建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
     **若要建立登入**  
  
    -   [建立登入](../../relational-databases/security/authentication-access/create-a-login.md)  
  
    -   [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)  
  
2.  (選擇性) 將 VIEW SERVER STATE 授與這個登入。  
  
    -   [GRANT 系統物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)  
  
     如需詳細資訊，請參閱 [GRANT 資料庫主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)。  
  
3.  針對這個登入建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者。  
  
     **建立使用者**  
  
    -   [建立資料庫使用者](../../relational-databases/security/authentication-access/create-a-database-user.md)  
  
    -   [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)  
  
4.  若要讓這個登入和使用者的工作階段備份給定的資料庫，請將使用者加入至該資料庫的 db_backupoperator 資料庫角色。 請針對這位使用者將備份的每個資料庫執行此步驟。 (選擇性) 將使用者加入至其他固定資料庫角色。  
  
     **將使用者加入至固定資料庫角色**  
  
    -   [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)  
  
     如需詳細資訊，請參閱 [GRANT 資料庫主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)。  
  
### <a name="example-a-setting-up-a-login-and-user-transact-sql"></a>範例 A：設定登入和使用者 (Transact-SQL)  
 只有當您選擇針對低優先權備份建立新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和使用者時，下列範例才會相關。 或者，您也可以使用現有的登入和使用者 (如果適當項目存在的話)。  
  
> [!IMPORTANT]  
>  下列範例會使用範例登入和使用者名稱 *domain_name*`\MAX_CPU`。 請將這些名稱取代成您打算在建立低優先順序壓縮備份時使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和使用者名稱。  
  
 這個範例會針對 *domain_name*`\MAX_CPU` Windows 帳戶建立登入，然後將 VIEW SERVER STATE 權限授與此登入。 這個權限可讓您確認登入工作階段的資源管理員分類。 然後，此範例會針對 *domain_name*`\MAX_CPU` 建立使用者並將它加入至 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 範例資料庫的 db_backupoperator 固定資料庫角色。 資源管理員分類函數將會使用這個使用者名稱。  
  
```tsql  
-- Create a SQL Server login for low-priority operations  
USE master;  
CREATE LOGIN [domain_name\MAX_CPU] FROM WINDOWS;  
GRANT VIEW SERVER STATE TO [domain_name\MAX_CPU];  
GO  
-- Create a SQL Server user in AdventureWorks2012 for this login  
USE AdventureWorks2012;  
CREATE USER [domain_name\MAX_CPU] FOR LOGIN [domain_name\MAX_CPU];  
EXEC sp_addrolemember 'db_backupoperator', 'domain_name\MAX_CPU';  
GO  
  
```  
  
 [&#91;回到頁首&#93;](#Top)  
  
##  <a name="configure_RG"></a> 設定資源管理員來限制 CPU 使用量  
  
> [!NOTE]  
>  請確定資源管理員已啟用。 如需詳細資訊，請參閱 [啟用資源管理員](../../relational-databases/resource-governor/enable-resource-governor.md)。  
  
 在這個資源管理員狀況中，組態設定包含下列基本步驟：  
  
1.  建立和設定資源管理員資源集區，以便在發生 CPU 競爭時，限制提供給資源集區中要求的最大平均 CPU 頻寬。  
  
2.  建立和設定使用這個集區的資源管理員工作負載群組。  
  
3.  建立 *「分類函數」*(Classifier Function)，它是使用者定義的函數 (UDF)，而且資源管理員會使用其傳回值來分類工作階段，以便將它們路由傳送至適當的工作負載群組。  
  
4.  向資源管理員註冊此分類函數。  
  
5.  將這些變更套用至資源管理員的記憶體中組態。  
  
> [!NOTE]  
>  如需有關資源管理員資源集區、工作負載群組和分類的相關資訊，請參閱 [資源管理員](../../relational-databases/resource-governor/resource-governor.md)。  
  
 這些步驟的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式將在「設定資源管理員來限制 CPU 使用量」程序中說明，而且後面接著該程序的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 範例。  
  
 **設定資源管理員 (SQL Server Management Studio)**  
  
-   [使用範本來設定資源管理員](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)  
  
-   [建立資源集區](../../relational-databases/resource-governor/create-a-resource-pool.md)  
  
-   [建立工作負載群組](../../relational-databases/resource-governor/create-a-workload-group.md)  
  
### <a name="to-configure-resource-governor-for-limiting-cpu-usage-transact-sql"></a>設定資源管理員來限制 CPU 使用量 (Transact-SQL)  
  
1.  發出 [CREATE RESOURCE POOL](../../t-sql/statements/create-resource-pool-transact-sql.md) 陳述式來建立資源集區。 這個程序的範例會使用下列語法：  
  
     *CREATE RESOURCE POOL pool_name* WITH ( MAX_CPU_PERCENT = *value* );  
  
     *Value* 是介於 1 和 100 之間的整數，表示最大平均 CPU 頻寬的百分比。 適當的值會因您的環境而不同。 為了方便說明，這個主題中的範例會使用 20% percent (MAX_CPU_PERCENT = 20)。  
  
2.  發出 [CREATE WORKLOAD GROUP](../../t-sql/statements/create-workload-group-transact-sql.md) 陳述式，針對您想要管理其 CPU 使用量的低優先權作業建立工作負載群組。 這個程序的範例會使用下列語法：  
  
     CREATE WORKLOAD GROUP *group_name* USING *pool_name*;  
  
3.  發出 [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) 陳述式來建立分類函數，以便將上述步驟中建立工作負載群組對應至低優先權登入的使用者。 這個程序的範例會使用下列語法：  
  
     CREATE FUNCTION [*schema_name*.]*function_name*() RETURNS sysname  
  
     WITH SCHEMABINDING  
  
     AS  
  
     BEGIN  
  
     DECLARE @workload_group_name AS *sysname*  
  
     IF (SUSER_NAME() = '*user_of_low_priority_login*')  
  
     SET @workload_group_name = '*workload_group_name*'  
  
     RETURN @workload_group_name  
  
     END  
  
     如需有關這個 CREATE FUNCTION 陳述式之元件的詳細資訊，請參閱：  
  
    -   [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
  
    -   [SUSER_SNAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sname-transact-sql.md)  
  
        > [!IMPORTANT]  
        >  SUSER_NAME 只是可用於分類函數的其中一個系統函數。 如需詳細資訊，請參閱 [建立和測試分類使用者定義函數](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)。  
  
    -   [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)。  
  
4.  發出 [ALTER RESOURCE GOVERNOR](../../t-sql/statements/alter-resource-governor-transact-sql.md) 陳述式，向資源管理員註冊此分類函數。 這個程序的範例會使用下列語法：  
  
     ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION = *schema_name*.*function_name*);  
  
5.  發出第二個 ALTER RESOURCE GOVERNOR 陳述式，將這些變更套用至資源管理員的記憶體中組態，如下所示：  
  
    ```  
    ALTER RESOURCE GOVERNOR RECONFIGURE;  
    ```  
  
### <a name="example-b-configuring-resource-governor-transact-sql"></a>範例 B：設定資源管理員 (Transact-SQL)  
 下列範例會在單一交易中執行下列步驟：  
  
1.  建立 `pMAX_CPU_PERCENT_20` 資源集區。  
  
2.  建立 `gMAX_CPU_PERCENT_20` 工作負載群組。  
  
3.  建立 `rgclassifier_MAX_CPU()` 分類函數，而且它會使用在上述範例中建立的使用者名稱。  
  
4.  向資源管理員註冊此分類函數。  
  
 認可交易之後，此範例就會套用在 ALTER WORKLOAD GROUP 或 ALTER RESOURCE POOL 陳述式中要求的組態變更。  
  
> [!IMPORTANT]  
>  下列範例會使用在＜範例 A：設定登入和使用者 (Transact-SQL)＞中建立之範例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者的使用者名稱 *domain_name*`\MAX_CPU`。 請將這個名稱取代成您打算在建立低優先順序壓縮備份時使用的登入使用者名稱。  
  
```tsql  
-- Configure Resource Governor.  
BEGIN TRAN  
USE master;  
-- Create a resource pool that sets the MAX_CPU_PERCENT to 20%.   
CREATE RESOURCE POOL pMAX_CPU_PERCENT_20  
   WITH  
      (MAX_CPU_PERCENT = 20);  
GO  
-- Create a workload group to use this pool.   
CREATE WORKLOAD GROUP gMAX_CPU_PERCENT_20  
USING pMAX_CPU_PERCENT_20;  
GO  
-- Create a classification function.  
-- Note that any request that does not get classified goes into   
-- the 'Default' group.  
CREATE FUNCTION dbo.rgclassifier_MAX_CPU() RETURNS sysname   
WITH SCHEMABINDING  
AS  
BEGIN  
    DECLARE @workload_group_name AS sysname  
      IF (SUSER_NAME() = 'domain_name\MAX_CPU')  
          SET @workload_group_name = 'gMAX_CPU_PERCENT_20'  
    RETURN @workload_group_name  
END;  
GO  
  
-- Register the classifier function with Resource Governor.  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION= dbo.rgclassifier_MAX_CPU);  
COMMIT TRAN;  
GO  
-- Start Resource Governor  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
  
```  
  
 [&#91;回到頁首&#93;](#Top)  
  
##  <a name="verifying"></a> 確認目前工作階段的分類 (Transact-SQL)  
 (選擇性) 以您在分類函數中指定之使用者的身分登入，然後在 [物件總管] 中發出下列 [SELECT](../../t-sql/queries/select-transact-sql.md) 陳述式，藉以確認工作階段分類：  
  
```tsql  
USE master;  
SELECT sess.session_id, sess.login_name, sess.group_id, grps.name   
FROM sys.dm_exec_sessions AS sess   
JOIN sys.dm_resource_governor_workload_groups AS grps   
    ON sess.group_id = grps.group_id  
WHERE session_id > 50;  
GO  
```  
  
 在結果窗格中，**名稱**資料行應該會針對您在分類函數中指定的工作負載群組名稱，列出一或多個工作階段。  
  
> [!NOTE]  
>  如需此 SELECT 陳述式呼叫的動態管理檢視相關資訊，請參閱 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) 和 [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)。  
  
 [&#91;頁首&#93;](#Top)  
  
##  <a name="creating_compressed_backup"></a> 使用含有限制 CPU 的工作階段來壓縮備份  
 若要在含有限制最大 CPU 的工作階段中建立壓縮備份，請以您在分類函數中指定之使用者的身分登入。 在備份命令中，指定 WITH COMPRESSION ([!INCLUDE[tsql](../../includes/tsql-md.md)]) 或選取 [壓縮備份] ([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)])。 若要建立壓縮的資料庫備份，請參閱[建立完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)。  
  
### <a name="example-c-creating-a-compressed-backup-transact-sql"></a>範例 C：建立壓縮備份 (Transact-SQL)  
 下列 [BACKUP](../../t-sql/statements/backup-transact-sql.md) 範例會在最近格式化的備份檔案 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 中建立 `Z:\SQLServerBackups\AdvWorksData.bak`資料庫的完整壓縮備份。  
  
```tsql  
--Run backup statement in the gBackup session.  
BACKUP DATABASE AdventureWorks2012 TO DISK='Z:\SQLServerBackups\AdvWorksData.bak'   
WITH   
   FORMAT,   
   MEDIADESCRIPTION='AdventureWorks2012 Compressed Data Backups'  
   DESCRIPTION='First database backup on AdventureWorks2012 Compressed Data Backups media set'  
   COMPRESSION;  
GO  
```  
  
 [&#91;回到頁首&#93;](#Top)  
  
## <a name="see-also"></a>另請參閱  
 [建立和測試分類使用者定義函數](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)   
 [資源管理員](../../relational-databases/resource-governor/resource-governor.md)  
  
  
