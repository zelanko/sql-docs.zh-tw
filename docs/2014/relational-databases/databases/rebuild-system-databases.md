---
title: 重建系統資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- master database [SQL Server], rebuilding
- REBUILDDATABASE parameter
- rebuilding databases, master
- system databases [SQL Server], rebuilding
ms.assetid: af457ecd-523e-4809-9652-bdf2e81bd876
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b58378e8ba2193a186fb58e3e784bf9bc3cb4d4c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62871265"
---
# <a name="rebuild-system-databases"></a>重建系統資料庫
  您必須重建系統資料庫，才能在 [master](master-database.md)、 [model](model-database.md)、 [msdb](msdb-database.md)或 [resource](resource-database.md) 系統資料庫中修正損毀問題，或修改預設的伺服器層級定序。 本主題將提供在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中重建系統資料庫的逐步指示。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [必要條件](#Prerequisites)  
  
-   **程序：**  
  
     [重建系統資料庫](#RebuildProcedure)  
  
     [重建資源資料庫](#Resource)  
  
     [建立新的 msdb 資料庫](#CreateMSDB)  
  
-   **後續操作：**  
  
     [疑難排解重建錯誤](#Troubleshoot)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
 重建 master、model、msdb 和 tempdb 系統資料庫時，系統會在這些資料庫的原始位置中卸除並重新建立它們。 如果您在重建陳述式中指定了新的定序，系統就會使用該定序設定來建立系統資料庫。 使用者對這些資料庫所做的任何修改都將遺失。 例如，您可能會在 master 資料庫中設有使用者定義的物件、在 msdb 中設有排程的作業，或在 model 資料庫中變更預設資料庫設定。  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
 請在重建系統資料庫之前執行下列工作，以便確保您可以將系統資料庫還原成目前的設定。  
  
1.  記錄所有伺服器範圍的組態值。  
  
    ```  
    SELECT * FROM sys.configurations;  
    ```  
  
2.  記錄所有套用至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 Service Pack 和 Hotfix 以及目前的定序。 您必須在重建系統資料庫之後重新套用這些更新。  
  
    ```  
    SELECT  
    SERVERPROPERTY('ProductVersion ') AS ProductVersion,  
    SERVERPROPERTY('ProductLevel') AS ProductLevel,  
    SERVERPROPERTY('ResourceVersion') AS ResourceVersion,  
    SERVERPROPERTY('ResourceLastUpdateDateTime') AS ResourceLastUpdateDateTime,  
    SERVERPROPERTY('Collation') AS Collation;  
    ```  
  
3.  記錄系統資料庫之所有資料和記錄檔的目前位置。 重建系統資料庫會將所有系統資料庫安裝到其原始位置。 如果您已將系統資料庫的資料或記錄檔移至不同的位置，就必須再次移動這些檔案。  
  
    ```  
    SELECT name, physical_name AS current_file_location  
    FROM sys.master_files  
    WHERE database_id IN (DB_ID('master'), DB_ID('model'), DB_ID('msdb'), DB_ID('tempdb'));  
    ```  
  
4.  找出 master、model 和 msdb 資料庫的目前備份。  
  
5.  如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體設定為複寫散發者，請找出散發資料庫的目前備份。  
  
6.  確定您擁有重建系統資料庫的適當權限。 若要執行這項作業，您必須是系統管理員 (`sysadmin`) 固定伺服器角色的成員。 如需詳細資訊，請參閱 [伺服器層級角色](../security/authentication-access/server-level-roles.md)。  
  
7.  確認 master、model 和 msdb 資料與記錄範本檔案的副本都存在本機伺服器上。 這些範本檔案的預設位置為 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn\Templates。 這些檔案會在重建程序期間使用，而且它們必須存在，才能讓安裝程式順利執行。 如果這些檔案已遺失，請執行安裝程式的修復功能，或手動從安裝媒體中複製這些檔案。 若要在安裝媒體上找到這些檔案，請巡覽至適當的平台目錄 (x86 或 x64)，然後巡覽至 setup\sql_engine_core_inst_msi\Pfiles\SqlServr\MSSQL.X\MSSQL\Binn\Templates。  
  
##  <a name="rebuild-system-databases"></a><a name="RebuildProcedure"></a> 重建系統資料庫  
 下列程序會重建 master、model、msdb 和 tempdb 系統資料庫。 您無法指定要重建的系統資料庫。 若為叢集執行個體，您必須在使用中節點上執行此程序，而且必須先讓對應叢集應用程式群組中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源離線，然後再執行此程序。  
  
 這項程序不會重建 resource 資料庫。 請參閱本主題後面的＜重建 resource 資料庫程序＞一節。  
  
#### <a name="to-rebuild-system-databases-for-an-instance-of-sql-server"></a>若要重建 SQL Server 執行個體的系統資料庫：  
  
1.  將 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝媒體插入光碟機，或在命令提示字元中，將目錄變更為本機伺服器上 setup.exe 檔案的位置。 伺服器的預設位置是 C:\Program Files\Microsoft SQL Server\120\Setup Bootstrap\Release。  
  
2.  在 [命令提示字元] 視窗中，輸入下列命令。 方括號是用來表示選擇性參數。 請勿輸入方括號。 使用啟用使用者帳戶控制 (UAC) 的 Windows 作業系統時，必須要有更高的權限才能執行安裝程式。 您必須以管理員的身分執行命令提示字元。  
  
     `Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName /SQLSYSADMINACCOUNTS=accounts [ /SAPWD= StrongPassword ] [ /SQLCOLLATION=CollationName]`  
  
    |參數名稱|描述|  
    |--------------------|-----------------|  
    |/QUIET 或 /Q|指定安裝程式的執行不使用任何使用者介面。|  
    |/ACTION=REBUILDDATABASE|指定安裝程式要重新建立系統資料庫。|  
    |/INSTANCENAME =*INSTANCENAME*|這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的名稱。 若為預設執行個體，請輸入 MSSQLSERVER。|  
    |/SQLSYSADMINACCOUNTS=*accounts*|指定要加入至系統管理員 (`sysadmin`) 固定伺服器角色的 Windows 群組或個別帳戶。 指定多個帳戶時，請以空格隔開這些帳戶。 例如，您可以輸入 **BUILTIN\Administrators MyDomain\MyUser**。 當您要指定的帳戶在帳戶名稱中包含空白時，請以雙引號括住該帳戶。 例如，輸入 `NT AUTHORITY\SYSTEM`。|  
    |[ /SAPWD=*StrongPassword* ]|指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `sa`帳戶的密碼。 如果執行個體使用混合驗證 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 驗證) 模式，這就是必要的參數。<br /><br /> ** \* \*安全性\*注意事項**此`sa`帳戶是已知[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的帳戶，而且通常是惡意使用者的目標。 請務必針對 `sa` 登入使用一個增強式密碼。<br /><br /> 請勿針對 Windows 驗證模式指定此參數。|  
    |[ /SQLCOLLATION=*CollationName* ]|指定新的伺服器層級定序。 這是選擇性參數。 如果沒有指定，就會使用伺服器的目前定序。<br /><br /> ** \* \*重要\*事項**變更伺服器層級定序並不會變更現有使用者資料庫的定序。 所有新建立的使用者資料庫預設都會使用新的定序。<br /><br /> 如需詳細資訊，請參閱 [設定或變更伺服器定序](../collations/set-or-change-the-server-collation.md)。|  
  
3.  當安裝程式完成系統資料庫的重建作業時，它就會返回命令提示字元，而且不會顯示任何訊息。 您可以檢查 Summary.txt 記錄檔來確認此程序是否順利完成。 這個檔案位於 C:\Program Files\Microsoft SQL Server\120\Setup Bootstrap\Logs。  
  
## <a name="post-rebuild-tasks"></a>重建後的工作  
 重建資料庫之後，您可能必須執行下列額外的工作：  
  
-   還原 master、model 和 msdb 資料庫的最新完整備份。 如需詳細資訊，請參閱[系統資料庫的備份與還原 &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)。  
  
    > [!IMPORTANT]  
    >  如果您已變更伺服器定序，請勿還原系統資料庫。 這樣做會將新的定序取代成先前的定序設定。  
  
     如果無法使用備份，或者還原的備份並非最新備份，請重新建立任何遺漏的項目。 例如，請針對您的使用者資料庫、備份裝置、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入、端點等重新建立所有遺漏的項目。 重新建立項目的最佳方式是執行建立這些項目的原始指令碼。  
  
> [!IMPORTANT]  
>  我們建議您保護指令碼的安全，防止它們遭受未獲授權的人員更改。  
  
-   如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體設定為複寫散發者，您就必須還原散發資料庫。 如需詳細資訊，請參閱 [備份及還原複寫的資料庫](../replication/administration/back-up-and-restore-replicated-databases.md)。  
  
-   將系統資料庫移至您先前記錄的位置。 如需詳細資訊，請參閱 [移動系統資料庫](system-databases.md)。  
  
-   確認伺服器範圍的組態值符合您先前記錄的值。  
  
##  <a name="rebuild-the-resource-database"></a><a name="Resource"></a> 重建資源資料庫  
 下列程序會重建 resource 系統資料庫。 當您重建 resource 資料庫時，所有 Service Pack 和 Hotfix 都會遺失，因此必須重新套用。  
  
#### <a name="to-rebuild-the-resource-system-database"></a>若要重建 resource 系統資料庫：  
  
1.  從散發程式媒體啟動 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝程式 (setup.exe)。  
  
2.  在左側導覽區域中，按一下 **[維護]**，然後按一下 **[修復]**。  
  
3.  安裝程式支援規則和檔案常式將會執行，以便確保您的系統已安裝必要元件而且電腦通過安裝程式驗證規則。 按一下 **[確定]** 或 **[安裝]** 繼續進行。  
  
4.  在 [選取執行個體] 頁面上，選取要修復的執行個體，然後按 **[下一步]**。  
  
5.  修復規則將會執行，以便驗證作業。 若要繼續，請按 [下一步]****。  
  
6.  在 **[已完成修復準備工作]** 頁面中，按一下 **[修復]**。 [完成] 頁面會指出作業已完成。  
  
##  <a name="create-a-new-msdb-database"></a><a name="CreateMSDB"></a>建立新的 msdb 資料庫  
 如果`msdb`資料庫損毀，而且您沒有`msdb`資料庫的備份，您可以使用`msdb` **instmsdb**腳本來建立新的。  
  
> [!WARNING]  
>  使用 instmsdb `msdb`腳本重建資料庫**instmsdb**將會排除儲存在中`msdb`的所有資訊，例如作業、警示、操作員、維護計畫、備份歷程記錄、以原則為基礎的管理設定、Database Mail、效能資料倉儲等等。  
  
1.  停止所有連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的服務，包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent、 [!INCLUDE[ssRS](../../includes/ssrs.md)]、 [!INCLUDE[ssIS](../../includes/ssis-md.md)]，以及使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 做為資料存放區的所有應用程式。  
  
2.  使用命令 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 從命令列啟動 `NET START MSSQLSERVER /T3608`  
  
     如需詳細資訊，請參閱 [启动、停止、暂停、继续、重启 SQL Server 服务](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)。  
  
3.  在另一個命令列視窗中， `msdb`執行下列命令來卸離資料庫，並將* \<servername>* 取代為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的實例：`SQLCMD -E -S<servername> -dmaster -Q"EXEC sp_detach_db msdb"`  
  
4.  使用 Windows Explorer 重新命名`msdb`資料庫檔案。 根據預設，這些檔案位於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 DATA 子資料夾中。  
  
5.  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員正常停止並重新啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務。  
  
6.  在命令列視窗中，連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並執行命令： `SQLCMD -E -S<servername> -i"C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Install\instmsdb.sql" -o" C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Install\instmsdb.out"`  
  
     將* \<servername>* 取代為的實例。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的檔案系統路徑。  
  
7.  使用 [Windows 記事本] 開啟 **instmsdb.out** 檔，並檢查輸出是否有任何錯誤。  
  
8.  在執行個體上重新套用任何已安裝的 Service Pack 或 Hotfix。  
  
9. 重新建立儲存在`msdb`資料庫中的使用者內容，例如工作、警示等。  
  
10. 備份 `msdb` 資料庫。  
  
##  <a name="troubleshoot-rebuild-errors"></a><a name="Troubleshoot"></a> 疑難排解重建錯誤  
 語法和其他執行階段錯誤會顯示在 [命令提示字元] 視窗中。 您可以檢查安裝程式陳述式是否有下列語法錯誤：  
  
-   在每個參數名稱前面遺漏了斜線 (/)。  
  
-   在參數名稱與參數值之間遺漏了等號 (=)。  
  
-   在參數名稱與等號之間存在空格。  
  
-   存在逗號 (,) 或語法中並未指定的其他字元。  
  
 重建作業完成之後，請檢查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄檔是否有任何錯誤。 預設記錄檔位置是 C:\Program Files\Microsoft SQL Server\120\Setup Bootstrap\Logs。 若要找出包含重建程序結果的記錄檔，請在命令提示字元中，將目錄變更為 Logs 資料夾，然後執行 `findstr /s RebuildDatabase summary*.*`。 這項搜尋將會為您指出包含重建系統資料庫結果的任何記錄檔。 您可以開啟這些記錄檔，然後檢查它們是否有相關的錯誤訊息。  
  
## <a name="see-also"></a>另請參閱  
 [系統資料庫](system-databases.md)  
  
  
