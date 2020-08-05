---
title: sqlmaint 公用程式
description: 在 SQL Server 中，使用 sqlmaint 來執行 DBCC 檢查、備份資料庫與其交易記錄、更新統計資料，以及重建索引。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- database maintenance plans [SQL Server]
- sqlmaint utility
- maintaining databases [SQL Server]
- backups [SQL Server], sqlmaint utility
- command prompt utilities [SQL Server], sqlmaint
- maintenance plans [SQL Server], command prompt
- backing up [SQL Server], sqlmaint utility
ms.assetid: 937a9932-4aed-464b-b97a-a5acfe6a50de
author: markingmyname
ms.author: maghan
ms.openlocfilehash: aaa935a955610ce5acb75a4b70141f8252cb3092
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918345"
---
# <a name="sqlmaint-utility"></a>sqlmaint 公用程式
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]
  如果**sqlmaint** 公用程式會在一或多個資料庫上，執行一組指定的維護作業。 利用 **sqlmaint** 來執行 DBCC 檢查、備份資料庫及其交易記錄、更新統計資料，以及重建索引。 所有資料庫維護活動都會產生一份可傳給指定文字檔、HTML 檔或電子郵件帳戶的報表。 **sqlmaint** 會執行舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]所建立的資料庫維護計畫。 若要從命令提示字元執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 維護計畫，請使用 [dtexec 公用程式](../integration-services/packages/dtexec-utility.md)。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../includes/ssnotedepnextavoid-md.md)] 請改用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 維護計畫功能。 如需維護計畫的詳細資訊，請參閱 [維護計畫](../relational-databases/maintenance-plans/maintenance-plans.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqlmaint   
[-?] |  
[  
     [-S server_name[\instance_name]]  
     [-U login_ID [-P password]]  
     {  
          [-D database_name | -PlanName name | -PlanID guid ]  
          [-Rpt text_file]  
          [-To operator_name]  
          [-HtmlRpt html_file [-DelHtmlRpt <time_period>] ]  
          [-RmUnusedSpace threshold_percentfree_percent]  
          [-CkDB | -CkDBNoIdx]  
          [-CkAl | -CkAlNoIdx]  
          [-CkCat]  
          [-UpdOptiStats sample_percent]  
          [-RebldIdx free_space]  
          [-SupportComputedColumn]  
          [-WriteHistory]  
          [  
               {-BkUpDB [backup_path] | -BkUpLog [backup_path] }  
               {-BkUpMedia  
                    {DISK [  
                           [-DelBkUps <time_period>]   
                           [-CrBkSubDir ]   
                           [-UseDefDir ]   
                          ]  
                     | TAPE   
                    }  
               }  
               [-BkUpOnlyIfClean]  
               [-VrfyBackup]  
          ]  
     }  
]  
<time_period> ::=  
number[minutes | hours | days | weeks | months]  
```  
  
## <a name="arguments"></a>引數  
 參數和值必須用空格分隔。 例如， **-S** 和 *server_name*之間必須有一個空格。  
  
 **-?**  
 指定傳回 **sqlmaint** 的語法圖。 這個參數必須單獨使用。  
  
 **-S** _server_name_[ **\\** _instance\_name_]  
 指定 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的目標執行個體。 指定 _server\_name_，即可連接到該伺服器上 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的預設執行個體。 指定 _server\_name_ **\\** _instance\_name_，即可連線到該伺服器上 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的具名執行個體。 如果未指定伺服器， **sqlmaint** 會連接到本機電腦中 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的預設執行個體。  
  
 **-U** _login_ID_  
 指定連接伺服器時所用的登入識別碼。 如果未提供， **sqlmaint** 會嘗試使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 驗證。 如果 *login_ID* 包含特殊字元，則必須以雙引號 (") 括住；否則可省略雙引號。  
  
> [!IMPORTANT]  
>  盡可能使用 Windows 驗證。  
  
 **-P** _password_  
 指定登入識別碼的密碼。 只有在同時提供 **-U** 參數時，這才有效。 如果 *password* 包含特殊字元，則必須將此引數括在雙引號內，否則可省略雙引號。  
  
> [!IMPORTANT]  
>  密碼不會有遮罩。 盡可能使用 Windows 驗證。  
  
 **-D** _database_name_  
 指定要執行維護作業的資料庫名稱。 如果 *database_name* 包含特殊字元，則必須以雙引號括住；否則可省略雙引號。  
  
 **-PlanName** _name_  
 指定利用資料庫維護計畫精靈定義的資料庫維護計畫名稱。 **sqlmaint** 所用的計畫資訊，只有計畫中的資料庫清單。 您在其他 **sqlmaint** 參數中指定的任何維護活動，都會套用到此資料庫清單。  
  
 **-PlanID** _guid_  
 指定利用資料庫維護計畫精靈定義之資料庫維護計畫的全域唯一識別碼 (GUID)。 **sqlmaint** 所用的計畫資訊，只有計畫中的資料庫清單。 您在其他 **sqlmaint** 參數中指定的任何維護活動，都會套用到此資料庫清單。 這必須符合 msdb.dbo.sysdbmaintplans 中的 plan_id 值。  
  
 **-Rpt** _text_file_  
 指定要產生報表之檔案的完整路徑和名稱。 報表也會出現在畫面中。 這份報表會在檔案名稱中附加日期來維護版本資訊。 日期的產生方式如下：在檔案名稱的尾端、英文句點的前面，格式如下：_*yyyyMMddhhmm*。 *yyyy* = 年、 *MM* = 月、 *dd* = 日、 *hh* = 時、 *mm* = 分。  
  
 如果您在 1996 年 12 月 1 日上午 10:23 執行這個公用程式，則 *text_file* 值如下：  
  
```  
c:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint.rpt  
```  
  
 產生的檔案名稱如下：  
  
```  
c:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint_199612011023.rpt  
```  
  
 當 *sqlmaint* 存取遠端伺服器時，需要 **text_file** 的完整通用命名慣例 (UNC) 檔案名稱。  
  
 **-To**  _operator_name_  
 指定將接收 SQL Mail 所產生之報表的操作員。  
  
 **-HtmlRpt** _html_file_  
 指定要產生 HTML 報表之檔案的完整路徑和名稱。 **sqlmaint** 也會在檔案名稱中附加 _*yyyyMMddhhmm* 格式的字串來產生檔案名稱，就像其對 **-Rpt** 參數所做的。  
  
 當 *sqlmaint* 存取遠端伺服器時，需要 **html_file** 的完整 UNC 檔案名稱。  
  
 **-DelHtmlRpt** \<*time_period*>  
 指定如果建立報表檔之後的時間間隔超出 \<*time_period*>，便刪除報表目錄中的任何 HTML 報表。 **-DelHtmlRpt** 會尋找名稱符合 *html_file* 參數所產生之模式的檔案。 如果 *html_file* 是 c:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint.htm，則 **-DelHtmlRpt** 會導致 **sqlmaint** 刪除名稱符合 C:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint\*.htm 模式，而且比指定的 \<*time_period*> 還舊的所有檔案。  
  
 **-RmUnusedSpace** _threshold_percent free_percent_  
 指定從 **-D**指定的資料庫中移除未使用的空間。 這個選項只適用於定義成自動成長的資料庫。 *Threshold_percent* 會以 MB 為單位來指定大小，一旦資料庫到達此大小之後， **sqlmaint** 便會嘗試移除未使用的資料空間。 在資料庫大小小於 *threshold_percent*時，則不會採取任何動作。 *Free_percent* 會指定必須保留在資料庫中的未使用空間大小，指定的方式是資料庫最終大小的百分比。 例如，如果 200 MB 資料庫包含 100 MB 的資料， *free_percent* 指定 10 會使最終資料庫大小成為 110 MB。 請注意，如果資料庫小於 *free_percent* 加上資料庫中的資料量，就不會擴充資料庫。 例如，如果 108 MB 的資料庫包含 100 MB 的資料， *free_percent* 指定 10 並不會將資料庫擴充成 110 MB；它會保持 108 MB。  
  
 **-CkDB** |  **-CkDBNoIdx**  
 指定在 **-D**所指定的資料庫中，執行設定了 NOINDEX 選項的 DBCC CHECKDB 陳述式或 DBCC CHECKDB 陳述式。 如需詳細資訊，請參閱 DBCC CHECKDB。  
  
 如果執行 *sqlmaint* 時資料庫正在使用中，就會在 **text_file** 中寫入一則警告。  
  
 **-CkAl** |  **-CkAlNoIdx**  
 指定在 **-D**所指定的資料庫中，執行設定了 NOINDEX 選項的 DBCC CHECKALLOC 陳述式。 如需詳細資訊，請參閱 [DBCC CHECKALLOC &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)。  
  
 **-CkCat**  
 指定在 **-D** 所指定的資料庫中，執行 DBCC CHECKCATALOG (Transact-SQL) 陳述式。 如需詳細資訊，請參閱 [DBCC CHECKCATALOG &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md)。  
  
 **-UpdOptiStats** _sample_percent_  
 指定在資料庫的各份資料表上，執行下列陳述式：  
  
```  
UPDATE STATISTICS table WITH SAMPLE sample_percent PERCENT;  
```  
  
 如果資料表包含計算資料行，當您使用 **-UpdOptiStats** 時，也必須指定 **-SupportedComputedColumn**引數。  
  
 如需詳細資訊，請參閱 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../t-sql/statements/update-statistics-transact-sql.md)所建立的資料庫維護計畫。  
  
 **-RebldIdx** _free_space_  
 指定應該利用 *free_space* 百分比值作為填滿因數的反項，藉以重建目標資料庫中各資料表的索引。 例如，如果 *free_space* 百分比是 30，則使用的填滿因數就是 70。 如果將 *free_space* 百分比值指定為 100，則會使用原始的填滿因數值來重建索引。  
  
 如果索引位於計算資料行上，當您使用 **-RebldIdx** 時，也必須指定 **-SupportComputedColumn**引數。  
  
 **-RebldIdx**  
 必須指定此引數，才能在計算資料行上，利用 **sqlmaint** 來執行 DBCC 維護命令。  
  
 **-WriteHistory**  
 指定在 msdb.dbo.sysdbmaintplan_history 中， **sqlmaint**所執行的每個維護動作都要建立一個項目。 如果指定了 **-PlanName** 或 **-PlanID** ，sysdbmaintplan_history 中的項目便會使用指定計畫的識別碼。 如果指定了 **-D** ，就會用幾個零做為計畫識別碼來建立 sysdbmaintplan_history 中的項目。  
  
 **-BkUpDB** [ *backup_path*] |  **-BkUpLog** [ *backup_path* ]  
 指定備份動作。 **-BkUpDb** 會備份整個資料庫。 **-BkUpLog** 只會備份交易記錄。  
  
 *backup_path* 會指定備份目錄。 如果也指定了*backup_path* ，便不需要 **backup_path** ，如果同時指定這兩者， **backup_path** 就會覆寫 backup_path。 備份可以放在目錄或磁帶裝置位址 (例如 \\\\.\TAPE0) 中。 資料庫備份的檔案名稱會依照下列方式自動產生：  
  
```  
dbname_db_yyyyMMddhhmm.BAK  
  
```  
  
 其中  
  
-   *dbname* 是正在備份的資料庫名稱。  
  
-   *yyyyMMddhhmm* 是備份作業的時間， *yyyy* = 年、 *MM* = 月、 *dd* = 日、 *hh* = 時，以及 *mm* = 分。  
  
 交易備份的檔案名稱也會利用類似的格式自動產生：  
  
```  
dbname_log_yyyymmddhhmm.BAK  
  
```  
  
 如果您使用 **-BkUpDB** 參數，也必須使用 **-BkUpMedia** 參數來指定媒體。  
  
 **-BkUpMedia**  
 指定備份的媒體類型為 DISK 或 TAPE。  
  
 **DISK**  
 指定備份媒體是磁碟。  
  
 **-DelBkUps**< *time_period* >  
 針對磁碟備份，指定如果建立備份之後的時間間隔超出 \<*time_period*>，便會刪除備份目錄中的任何備份檔案。  
  
 **-CrBkSubDir**  
 對於磁碟備份，指定如果也指定了 *-UseDefDir*，便會在 [ **backup_path** ] 目錄或預設備份目錄中建立一個子目錄。 子目錄的名稱是從 **-D**指定的資料庫名稱所產生。 **-CrBkSubDir** 提供一種簡單的方式，讓您不需要變更 *backup_path* 參數，就能將不同資料庫的所有備份放在個別子目錄中。  
  
 **backup_path**  
 對於磁碟備份，指定在預設備份目錄中建立備份檔。 如果同時指定這兩者，則**UseDefDir** 會覆寫 *backup_path* 。 當採用預設的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安裝時，預設備份目錄是 C:\Program Files\Microsoft SQL Server\MSSQL10_50.MSSQLSERVER\MSSQL\Backup。  
  
 **TAPE**  
 指定備份媒體是磁帶。  
  
 **-BkUpOnlyIfClean**  
 指定只有在任何指定的 **-Ck** 檢查確定資料都沒問題時，才會進行備份。 維護動作會依照它們在命令提示字元下所呈現的順序來執行。 如果您還要指定 **-BkUpOnlyIfClean**，或者不論檢查是否報告問題都要執行備份，可在 **-BkUpDB**-BkUpLog **參數之前指定**-CkDB **、** -CkDBNoIdx **、** -CkAl **、** -CkAlNoIdx **、** / **-CkTxtAl** 或 **-CkCat**參數。  
  
 **-VrfyBackup**  
 指定在備份完成時執行 RESTORE VERIFYONLY。  
  
 *number*[**minutes**| **hours**| **day**| **weeks**| **months**]  
 指定一個時間間隔來決定報表或備份檔經過多久時間之後便可刪除。 *number* 是後面接著時間單位的一個整數 (不含空格)。 有效範例：  
  
-   **12weeks**  
  
-   **3months**  
  
-   **15days**  
  
 如果只指定 *number* ，預設的日期部分是 **weeks**。  
  
## <a name="remarks"></a>備註  
 **sqlmaint** 公用程式會在一或多個資料庫上執行維護作業。 如果指定了 **-D** ，就只會在指定的資料庫上執行其餘參數所指定的作業。 如果指定了 **-PlanName** 或 **-PlanID** ， **sqlmaint** 從指定的維護計畫中擷取的唯一資訊就是計畫中的資料庫清單。 從計畫中取得的清單所列出的每個資料庫，都會套用其餘 **sqlmaint** 參數所指定的所有作業。 **sqlmaint** 公用程式不會套用計畫本身所定義的任何維護活動。  
  
 如果 **sqlmaint** 公用程式順利執行，就會傳回 0，如果失敗，則傳回 1。 在下列情況下，會發出失敗報告：  
  
-   如果任何維護動作失敗。  
  
-   如果 **-CkDB**、 **-CkDBNoIdx**、 **-CkAl**、 **-CkAlNoIdx**、 **-CkTxtAl**或 **-CkCat** 檢查發現資料發生問題。  
  
-   如果發生一般失敗。  
  
## <a name="permissions"></a>權限  
 **sqlmaint** 公用程式可以由任何對於 **具有** 讀取和執行 `sqlmaint.exe`權限的 Windows 使用者執行，依預設，其會儲存於 `x:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER1\MSSQL\Binn` 資料夾內。 另外，以 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -login_ID **指定的** 登入必須擁有執行指定動作的必要 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 權限。 如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的連接是使用 Windows 驗證，則對應到已驗證之 Windows 使用者的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登入必須有執行指定動作的必要 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 權限。  
  
 例如，使用 **-BkUpDB** 需要有執行 BACKUP 陳述式的權限。 使用 **-UpdOptiStats** 引數需要有執行 UPDATE STATISTICS 陳述式的權限。 如需詳細資訊，請參閱線上叢書中對應主題的＜權限＞章節。  
  
## <a name="examples"></a>範例  
  
### <a name="a-performing-dbcc-checks-on-a-database"></a>A. 在資料庫中執行 DBCC 檢查  
  
```  
sqlmaint -S MyServer -D AdventureWorks2012 -CkDB -CkAl -CkCat -Rpt C:\MyReports\AdvWks_chk.rpt  
```  
  
### <a name="b-updating-statistics-using-a-15-sample-in-all-databases-in-a-plan-also-shrink-any-of-the-database-that-have-reached-110-mb-to-having-only-10-free-space"></a>B. 在計畫的所有資料庫中，利用 15% 取樣來更新統計資料。 另外，將到達 110 MB 的任何資料庫壓縮成只有 10% 的可用空間  
  
```  
sqlmaint -S MyServer -PlanName MyUserDBPlan -UpdOptiStats 15 -RmUnusedSpace 110 10  
```  
  
### <a name="c-backing-up-all-the-databases-in-a-plan-to-their-individual-subdirectories-in-the-default-xprogram-filesmicrosoft-sql-servermssql13mssqlservermssqlbackup-directory-also-delete-any-backups-older-than-2-weeks"></a>C. 在預設的 x:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup 目錄中，將計畫中的所有資料庫備份到它們的個別子目錄中。 另外，如果備份比 2 星期還要舊，便予以刪除  
  
```  
sqlmaint -S MyServer -PlanName MyUserDBPlan -BkUpDB -BkUpMedia DISK -UseDefDir -CrBkSubDir -DelBkUps 2weeks  
```  
  
### <a name="d-backing-up-a-database-to-the-default-xprogram-filesmicrosoft-sql-servermssql13mssqlservermssqlbackup-directory"></a>D. 將資料庫備份到預設的 x:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup 目錄中。  
  
```  
sqlmaint -S MyServer -BkUpDB -BkUpMedia DISK -UseDefDir  
```  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](../t-sql/statements/backup-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../t-sql/statements/update-statistics-transact-sql.md)  
  
  
